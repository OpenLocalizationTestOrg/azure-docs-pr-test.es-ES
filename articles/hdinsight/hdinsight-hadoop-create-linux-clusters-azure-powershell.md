---
title: "clústeres de Hadoop de aaaCreate con PowerShell, HDInsight de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate Hadoop, HBase, tormenta o Spark clusters en Linux para HDInsight mediante Azure PowerShell."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="46dc7-103">Crear clústeres basados en Linux en HDInsight con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46dc7-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="46dc7-104">Azure PowerShell es un entorno de scripting eficaz que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="46dc7-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="46dc7-105">Este documento proporciona información sobre cómo agrupar toocreate un HDInsight basados en Linux mediante el uso de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="46dc7-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="46dc7-106">También se incluye un script de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="46dc7-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="46dc7-107">Azure PowerShell solo está disponible en clientes de Windows.</span><span class="sxs-lookup"><span data-stu-id="46dc7-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="46dc7-108">Si utiliza un cliente de Mac OS X, Unix o Linux, consulte [crear un clúster de HDInsight basados en Linux mediante Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para obtener información acerca del uso de hello Azure CLI toocreate un clúster.</span><span class="sxs-lookup"><span data-stu-id="46dc7-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46dc7-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="46dc7-109">Prerequisites</span></span>
<span data-ttu-id="46dc7-110">Debe disponer de hello siguiente antes de iniciar este procedimiento:</span><span class="sxs-lookup"><span data-stu-id="46dc7-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="46dc7-111">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="46dc7-111">An Azure subscription.</span></span> <span data-ttu-id="46dc7-112">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="46dc7-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="46dc7-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46dc7-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="46dc7-114">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="46dc7-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="46dc7-115">Hola pasos de este documento use Hola nuevos cmdlets de HDInsight que funcionan con el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="46dc7-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="46dc7-116">Siga los pasos de hello en [instale Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) versión más reciente de hello tooinstall de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="46dc7-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="46dc7-117">Si tiene scripts de ese toobe necesidad de modifica toouse Hola nuevos cmdlets que funcionan con el Administrador de recursos de Azure, consulte [tooAzure desarrollo basado en el Administrador de recursos de migración de las herramientas de clústeres de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="46dc7-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="46dc7-118">Crear clúster</span><span class="sxs-lookup"><span data-stu-id="46dc7-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="46dc7-119">toocreate un clúster de HDInsight mediante el uso de PowerShell de Azure, debe completar Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="46dc7-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="46dc7-120">Creación de un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="46dc7-120">Create an Azure resource group</span></span>
* <span data-ttu-id="46dc7-121">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="46dc7-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="46dc7-122">Creación de un contenedor de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="46dc7-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="46dc7-123">Creación de un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="46dc7-124">Hello secuencia de comandos siguiente se muestra cómo toocreate un nuevo clúster:</span><span class="sxs-lookup"><span data-stu-id="46dc7-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="46dc7-125">valores de Hello especificados para el inicio de sesión de hello clúster son toocreate usado Hola cuenta de usuario de Hadoop para clústeres de Hola.</span><span class="sxs-lookup"><span data-stu-id="46dc7-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="46dc7-126">Utilice este tooservices de tooconnect cuenta hospedadas en clúster de hello como web API de REST o interfaces de usuario.</span><span class="sxs-lookup"><span data-stu-id="46dc7-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="46dc7-127">valores de Hello especificados para el usuario SSH de hello son usuario SSH de hello toocreate usado para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="46dc7-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="46dc7-128">Utilice esta cuenta toostart una sesión SSH remoto en clúster de Hola y ejecutar trabajos.</span><span class="sxs-lookup"><span data-stu-id="46dc7-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="46dc7-129">Para obtener más información, vea hello [utilizar SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="46dc7-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="46dc7-130">Si tiene previsto toouse más de 32 nodos de trabajador (en la creación del clúster o Hola escalado del clúster después de la creación), también debe especificar un tamaño de nodo principal con un mínimo de 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="46dc7-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="46dc7-131">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="46dc7-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="46dc7-132">Puede pasar hasta too20 minutos toocreate un clúster.</span><span class="sxs-lookup"><span data-stu-id="46dc7-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="46dc7-133">Creación de un clúster: objeto de configuración</span><span class="sxs-lookup"><span data-stu-id="46dc7-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="46dc7-134">También puede crear un objeto de configuración de HDInsight mediante el cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="46dc7-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="46dc7-135">A continuación, puede modificar estas opciones de configuración adicionales de tooenable de objeto de configuración para el clúster.</span><span class="sxs-lookup"><span data-stu-id="46dc7-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="46dc7-136">Por último, utilice hello `-Config` parámetro de hello `New-AzureRmHDInsightCluster` configuración de cmdlet toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="46dc7-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="46dc7-137">Hello script siguiente crea un tooconfigure de objeto de configuración un servidor de R en el tipo de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="46dc7-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="46dc7-138">configuración de Hello permite a un nodo del borde, RStudio y una cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="46dc7-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="46dc7-139">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="46dc7-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="46dc7-140">Cuando se usa en este ejemplo, crear cuenta de almacenamiento adicional de Hola Hola misma ubicación que el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="46dc7-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="46dc7-141">Personalización de los clústeres</span><span class="sxs-lookup"><span data-stu-id="46dc7-141">Customize clusters</span></span>

* <span data-ttu-id="46dc7-142">Consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="46dc7-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="46dc7-143">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="46dc7-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="46dc7-144">Eliminar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="46dc7-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="46dc7-145">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="46dc7-145">Troubleshoot</span></span>

<span data-ttu-id="46dc7-146">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="46dc7-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46dc7-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46dc7-147">Next steps</span></span>

<span data-ttu-id="46dc7-148">Ahora que ha creado correctamente un clúster de HDInsight, usar hello después cómo toolearn recursos toowork con el clúster.</span><span class="sxs-lookup"><span data-stu-id="46dc7-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="46dc7-149">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="46dc7-149">Hadoop clusters</span></span>

* [<span data-ttu-id="46dc7-150">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="46dc7-151">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="46dc7-152">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="46dc7-153">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="46dc7-153">HBase clusters</span></span>

* [<span data-ttu-id="46dc7-154">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="46dc7-155">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="46dc7-156">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="46dc7-156">Storm clusters</span></span>

* [<span data-ttu-id="46dc7-157">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="46dc7-158">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="46dc7-159">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="46dc7-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="46dc7-160">Clústeres de Spark</span><span class="sxs-lookup"><span data-stu-id="46dc7-160">Spark clusters</span></span>

* [<span data-ttu-id="46dc7-161">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="46dc7-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="46dc7-162">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="46dc7-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="46dc7-163">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="46dc7-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="46dc7-164">Spark con aprendizaje automático: Use Spark en HDInsight toopredict de resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="46dc7-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="46dc7-165">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="46dc7-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

