---
title: "clústeres de Hadoop de aaaCreate mediante la línea de comandos - Hola HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los clústeres de HDInsight de toocreate con Hola multiplataforma Azure CLI 1.0."
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="148ae-103">Crear clústeres de HDInsight con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="148ae-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="148ae-104">Hola pasos de este tutorial de documento creación de un clúster de HDInsight 3.5 con hello 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="148ae-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="148ae-105">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="148ae-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="148ae-106">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="148ae-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="148ae-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="148ae-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="148ae-108">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="148ae-108">**An Azure subscription**.</span></span> <span data-ttu-id="148ae-109">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="148ae-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="148ae-110">**CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="148ae-110">**Azure CLI**.</span></span> <span data-ttu-id="148ae-111">pasos de Hello en este documento se han probado última con CLI de Azure versión 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="148ae-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="148ae-112">pasos de Hello en este documento no funcionan con Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="148ae-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="148ae-113">La CLI de Azure 2.0 no admite la creación de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="148ae-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="148ae-114">Inicie sesión en tooyour suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="148ae-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="148ae-115">Siga los pasos de hello documentados en [conectarse tooan suscripción de Azure desde hello Azure interfaz de línea de comandos (CLI de Azure)](../xplat-cli-connect.md) y conectar suscripción tooyour con hello **inicio de sesión** método.</span><span class="sxs-lookup"><span data-stu-id="148ae-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="148ae-116">Crear un clúster</span><span class="sxs-lookup"><span data-stu-id="148ae-116">Create a cluster</span></span>

<span data-ttu-id="148ae-117">Hola pasos debe realizarse desde una línea de comandos, como PowerShell o Bash.</span><span class="sxs-lookup"><span data-stu-id="148ae-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="148ae-118">Usar hello después comando tooauthenticate tooyour suscripción de Azure:</span><span class="sxs-lookup"><span data-stu-id="148ae-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="148ae-119">Se está tooprovide solicitada su nombre y contraseña.</span><span class="sxs-lookup"><span data-stu-id="148ae-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="148ae-120">Si tiene varias suscripciones de Azure, use `azure account set <subscriptionname>` use comandos de suscripción de hello tooset que Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="148ae-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="148ae-121">Cambiar el modo de administrador de recursos de tooAzure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="148ae-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="148ae-122">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="148ae-122">Create a resource group.</span></span> <span data-ttu-id="148ae-123">Este grupo de recursos contiene el clúster de HDInsight de Hola y asociados de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="148ae-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="148ae-124">Reemplace `groupname` con un nombre único para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="148ae-125">Reemplace `location` con la región geográfica de Hola que desee toocreate hello en.</span><span class="sxs-lookup"><span data-stu-id="148ae-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="148ae-126">Para obtener una lista de ubicaciones válidas, usar hello `azure location list` comando y, a continuación, utilice una de las ubicaciones de Hola de hello `Name` columna.</span><span class="sxs-lookup"><span data-stu-id="148ae-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="148ae-127">Cree una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="148ae-127">Create a storage account.</span></span> <span data-ttu-id="148ae-128">Esta cuenta de almacenamiento se utiliza como almacenamiento predeterminado de hello para el clúster de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="148ae-129">Reemplace `groupname` con el nombre de hello del grupo de hello creado en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="148ae-130">Reemplace `location` con la misma ubicación que se utilizó en el paso anterior de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="148ae-131">Reemplace `storagename` con un nombre único para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="148ae-132">Para obtener más información sobre los parámetros de hello utilizados en este comando, use `azure storage account create -h` tooview ayuda para este comando.</span><span class="sxs-lookup"><span data-stu-id="148ae-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="148ae-133">Recuperar la cuenta de almacenamiento de Hola Hola clave tooaccess usado.</span><span class="sxs-lookup"><span data-stu-id="148ae-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="148ae-134">Reemplace `groupname` con el nombre de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="148ae-135">Reemplace `storagename` con el nombre de Hola de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="148ae-136">En datos de Hola que se devuelven, guardar hello `key` valor `key1`.</span><span class="sxs-lookup"><span data-stu-id="148ae-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="148ae-137">Cree un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="148ae-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="148ae-138">Reemplace `groupname` con el nombre de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="148ae-139">Reemplace `Hadoop` con el tipo de clúster de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="148ae-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="148ae-140">Por ejemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.</span><span class="sxs-lookup"><span data-stu-id="148ae-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="148ae-141">HDInsight clústeres proceden de diversos tipos, que corresponden a cargas de trabajo de toohello o tecnología de Hola clúster se optimiza para.</span><span class="sxs-lookup"><span data-stu-id="148ae-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="148ae-142">No hay ningún toocreate método admitido para un clúster que combina varios tipos, como Storm y HBase en un clúster.</span><span class="sxs-lookup"><span data-stu-id="148ae-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="148ae-143">Reemplace `location` con hello misma ubicación que se usa en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="148ae-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="148ae-144">Reemplace `storagename` con el nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="148ae-145">Reemplace `storagekey` con clave de hello obtenido en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="148ae-146">Para hello `--defaultStorageContainer` parámetro, Hola uso mismo nombre que se utilizan para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="148ae-147">Reemplace `admin` y `httppassword` con hello nombre y la contraseña que se va toouse al tener acceso a los clústeres de Hola a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="148ae-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="148ae-148">Reemplace `sshuser` y `sshuserpassword` con hello username y password desea toouse al tener acceso a clúster de hello mediante SSH</span><span class="sxs-lookup"><span data-stu-id="148ae-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="148ae-149">En este ejemplo se crea un clúster con dos nodos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="148ae-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="148ae-150">También puede cambiar número de Hola de nodos de trabajo después de la creación de clúster mediante la realización de operaciones de escala.</span><span class="sxs-lookup"><span data-stu-id="148ae-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="148ae-151">Si planea usar más de 32 nodos de trabajo, tiene que seleccionar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="148ae-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="148ae-152">Puede establecer el tamaño del nodo principal de hello mediante hello `--headNodeSize` parámetro durante la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="148ae-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="148ae-153">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="148ae-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="148ae-154">Puede tardar varios minutos para toofinish de proceso de creación de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="148ae-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="148ae-155">de creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="148ae-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="148ae-156">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="148ae-156">Troubleshoot</span></span>

<span data-ttu-id="148ae-157">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="148ae-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="148ae-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="148ae-158">Next steps</span></span>

<span data-ttu-id="148ae-159">Ahora que ha creado correctamente un clúster de HDInsight con hello CLI de Azure, use Hola sigue toolearn cómo toowork con el clúster:</span><span class="sxs-lookup"><span data-stu-id="148ae-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="148ae-160">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="148ae-160">Hadoop clusters</span></span>

* [<span data-ttu-id="148ae-161">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="148ae-162">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="148ae-163">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="148ae-164">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="148ae-164">HBase clusters</span></span>

* [<span data-ttu-id="148ae-165">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="148ae-166">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="148ae-167">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="148ae-167">Storm clusters</span></span>

* [<span data-ttu-id="148ae-168">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="148ae-169">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="148ae-170">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="148ae-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
