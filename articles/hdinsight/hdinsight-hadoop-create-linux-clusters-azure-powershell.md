---
title: "Creación de clústeres de Hadoop con PowerShell - Azure HDInsight | Microsoft Docs"
description: "Aprenda a crear clústeres de Hadoop, HBase, Storm o Spark en Linux para HDInsight con Azure PowerShell."
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="840b7-103">Crear clústeres basados en Linux en HDInsight con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="840b7-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="840b7-104">Azure PowerShell es un eficaz entorno de scripting que puede usar para controlar y automatizar la implementación y la administración de sus cargas de trabajo en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="840b7-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="840b7-105">En este documento se ofrece información sobre cómo crear un clúster de HDInsight basado en Linux mediante Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="840b7-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="840b7-106">También se incluye un script de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="840b7-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="840b7-107">Azure PowerShell solo está disponible en clientes de Windows.</span><span class="sxs-lookup"><span data-stu-id="840b7-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="840b7-108">Si está usando un cliente de Linux, Unix o Mac OS X, consulte [Crear clústeres basados en Linux en HDInsight con la CLI de Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para más información sobre el uso de la CLI de Azure para crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="840b7-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="840b7-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="840b7-109">Prerequisites</span></span>
<span data-ttu-id="840b7-110">Antes de iniciar este procedimiento, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="840b7-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="840b7-111">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="840b7-111">An Azure subscription.</span></span> <span data-ttu-id="840b7-112">Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="840b7-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="840b7-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="840b7-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="840b7-114">La compatibilidad con Azure PowerShell para administrar recursos de HDInsight mediante Azure Service Manager está **en desuso** y dejó de estar disponible por completo el 1 de enero de 2017.</span><span class="sxs-lookup"><span data-stu-id="840b7-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="840b7-115">En los pasos descritos en este documento, se usan los nuevos cmdlets de HDInsight que funcionan con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="840b7-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="840b7-116">Para instalar la última versión de Azure PowerShell, siga los pasos descritos en [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="840b7-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="840b7-117">Si tiene scripts que se deben modificar para usar los nuevos cmdlets que funcionan con Azure Resource Manager, consulte [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migración a herramientas de desarrollo basadas en Azure Resource Manager para clústeres de HDInsight) para más información.</span><span class="sxs-lookup"><span data-stu-id="840b7-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="840b7-118">Crear clúster</span><span class="sxs-lookup"><span data-stu-id="840b7-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="840b7-119">Para crear un clúster de HDInsight con Azure PowerShell, debe realizar los procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="840b7-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="840b7-120">Creación de un grupo de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="840b7-120">Create an Azure resource group</span></span>
* <span data-ttu-id="840b7-121">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="840b7-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="840b7-122">Creación de un contenedor de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="840b7-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="840b7-123">Creación de un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="840b7-124">El script siguiente muestra cómo crear un nuevo clúster:</span><span class="sxs-lookup"><span data-stu-id="840b7-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="840b7-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="840b7-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="840b7-126">Los valores que se especifican para el inicio de sesión de clúster se usan para crear la cuenta de usuario de Hadoop del clúster.</span><span class="sxs-lookup"><span data-stu-id="840b7-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="840b7-127">Use esta cuenta para conectarse a servicios hospedados en el clúster como interfaces de usuario web o API de REST.</span><span class="sxs-lookup"><span data-stu-id="840b7-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="840b7-128">Los valores que se especifican para el usuario SSH se usan para crear el usuario SSH para el clúster.</span><span class="sxs-lookup"><span data-stu-id="840b7-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="840b7-129">Use esta cuenta para iniciar una sesión remota de SSH en el clúster y ejecutar trabajos.</span><span class="sxs-lookup"><span data-stu-id="840b7-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="840b7-130">Para más información, vea el documento [Uso de SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="840b7-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="840b7-131">Si tiene pensado usar más de 32 nodos de trabajo (en el momento de crear el clúster o cambiando el tamaño del clúster después de su creación), también debe especificar un tamaño de nodo principal con al menos 8 núcleos y 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="840b7-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="840b7-132">Para obtener más información acerca de los tamaños de nodo y los costos asociados, consulte [Precios de HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="840b7-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="840b7-133">Un clúster puede tardar hasta 20 minutos en crearse.</span><span class="sxs-lookup"><span data-stu-id="840b7-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="840b7-134">Creación de un clúster: objeto de configuración</span><span class="sxs-lookup"><span data-stu-id="840b7-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="840b7-135">También puede crear un objeto de configuración de HDInsight mediante el cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="840b7-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="840b7-136">A continuación, puede modificar este objeto de configuración con el fin de habilitar otras opciones de configuración para el clúster.</span><span class="sxs-lookup"><span data-stu-id="840b7-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="840b7-137">Por último, utilice el parámetro `-Config` del cmdlet `New-AzureRmHDInsightCluster` para emplear la configuración.</span><span class="sxs-lookup"><span data-stu-id="840b7-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="840b7-138">El script siguiente crea un objeto de configuración para configurar un R Server en el tipo de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="840b7-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="840b7-139">La configuración habilita un nodo perimetral, RStudio y una cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="840b7-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="840b7-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="840b7-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="840b7-141">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="840b7-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="840b7-142">Cuando utilice este ejemplo, cree la cuenta de almacenamiento adicional en la misma ubicación que el servidor.</span><span class="sxs-lookup"><span data-stu-id="840b7-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="840b7-143">Personalización de los clústeres</span><span class="sxs-lookup"><span data-stu-id="840b7-143">Customize clusters</span></span>

* <span data-ttu-id="840b7-144">Consulte [Personalización de los clústeres de HDInsight con Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="840b7-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="840b7-145">Consulte [Personalización de clústeres de HDInsight mediante la acción de scripts](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="840b7-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="840b7-146">Eliminación del clúster</span><span class="sxs-lookup"><span data-stu-id="840b7-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="840b7-147">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="840b7-147">Troubleshoot</span></span>

<span data-ttu-id="840b7-148">Si experimenta problemas con la creación de clústeres de HDInsight, consulte los [requisitos de control de acceso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="840b7-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="840b7-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="840b7-149">Next steps</span></span>

<span data-ttu-id="840b7-150">Ahora que ya ha creado con éxito un clúster de HDInsight, use los siguientes recursos para aprender a trabajar con él.</span><span class="sxs-lookup"><span data-stu-id="840b7-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="840b7-151">Clústeres Hadoop</span><span class="sxs-lookup"><span data-stu-id="840b7-151">Hadoop clusters</span></span>

* [<span data-ttu-id="840b7-152">Uso de Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="840b7-153">Uso de Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="840b7-154">Uso de MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="840b7-155">Clústeres HBase</span><span class="sxs-lookup"><span data-stu-id="840b7-155">HBase clusters</span></span>

* [<span data-ttu-id="840b7-156">Introducción a HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="840b7-157">Desarrollo de aplicaciones de Java para HBase en HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="840b7-158">Clústeres Storm</span><span class="sxs-lookup"><span data-stu-id="840b7-158">Storm clusters</span></span>

* [<span data-ttu-id="840b7-159">Desarrollo de topologías de Java para Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="840b7-160">Uso de componentes de Python en Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="840b7-161">Implementación y supervisión de topologías con Storm en HDInsight</span><span class="sxs-lookup"><span data-stu-id="840b7-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="840b7-162">Clústeres de Spark</span><span class="sxs-lookup"><span data-stu-id="840b7-162">Spark clusters</span></span>

* [<span data-ttu-id="840b7-163">Crear una aplicación independiente con Scala</span><span class="sxs-lookup"><span data-stu-id="840b7-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="840b7-164">Ejecutar trabajos de forma remota en un clúster de Spark mediante Livy</span><span class="sxs-lookup"><span data-stu-id="840b7-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="840b7-165">Spark with BI: Realizar el análisis de datos interactivos con Spark en HDInsight con las herramientas de BI</span><span class="sxs-lookup"><span data-stu-id="840b7-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="840b7-166">Spark con aprendizaje automático: uso de Spark en HDInsight para predecir los resultados de la inspección de alimentos</span><span class="sxs-lookup"><span data-stu-id="840b7-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="840b7-167">Streaming con Spark: uso de Spark en HDInsight para compilar aplicaciones de streaming en tiempo real</span><span class="sxs-lookup"><span data-stu-id="840b7-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

