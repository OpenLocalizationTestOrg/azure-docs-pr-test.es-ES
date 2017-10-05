---
title: "Administración de clústeres de Hadoop en HDInsight con PowerShell: Azure | Microsoft Docs"
description: "Vea cómo realizar tareas administrativas para clústeres de Hadoop en HDInsight usando Azure PowerShell."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="2a902-103">Administración de clústeres de Hadoop en HDInsight con PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="2a902-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="2a902-104">Azure PowerShell es un potente entorno de scripting que puede usar para controlar y automatizar la implementación y la administración de sus cargas de trabajo en Azure.</span><span class="sxs-lookup"><span data-stu-id="2a902-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="2a902-105">En este artículo, aprenderá a administrar clústeres de Hadoop en HDInsight de Azure con una consola local de PowerShell de Azure mediante el uso de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a902-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="2a902-106">Para obtener más información sobre los cmdlets de PowerShell de HDInsight, consulte [Documentación de referencia de los cmdlets de HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="2a902-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="2a902-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="2a902-107">**Prerequisites**</span></span>

<span data-ttu-id="2a902-108">Antes de empezar este artículo, debe tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2a902-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="2a902-109">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="2a902-109">**An Azure subscription**.</span></span> <span data-ttu-id="2a902-110">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2a902-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="2a902-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a902-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="2a902-112">Si ha instalado la versión 0.9 x de Azure PowerShell, debe desinstalarla antes de instalar una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="2a902-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="2a902-113">Para comprobar la versión del PowerShell instalado:</span><span class="sxs-lookup"><span data-stu-id="2a902-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="2a902-114">Para desinstalar la versión anterior, ejecute Programas y características en el panel de control.</span><span class="sxs-lookup"><span data-stu-id="2a902-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="2a902-115">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="2a902-115">Create clusters</span></span>
<span data-ttu-id="2a902-116">Consulte [Crear clústeres basados en Linux en HDInsight con Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="2a902-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="2a902-117">Enumeración de clústeres</span><span class="sxs-lookup"><span data-stu-id="2a902-117">List clusters</span></span>
<span data-ttu-id="2a902-118">Use el comando siguiente para enumerar todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="2a902-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="2a902-119">Presentación de clústeres</span><span class="sxs-lookup"><span data-stu-id="2a902-119">Show cluster</span></span>
<span data-ttu-id="2a902-120">Use el comando siguiente para mostrar los detalles de un clúster específico de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="2a902-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="2a902-121">Eliminación de clústeres</span><span class="sxs-lookup"><span data-stu-id="2a902-121">Delete clusters</span></span>
<span data-ttu-id="2a902-122">Use el comando siguiente para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="2a902-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="2a902-123">También puede eliminar un clúster quitando el grupo de recursos que contiene el clúster.</span><span class="sxs-lookup"><span data-stu-id="2a902-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="2a902-124">Tenga en cuenta que esto eliminará todos los recursos del grupo, incluida la cuenta de almacenamiento predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2a902-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="2a902-125">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="2a902-125">Scale clusters</span></span>
<span data-ttu-id="2a902-126">La característica de escalado de clústeres permite cambiar la cantidad de nodos de trabajo que usa un clúster que se ejecuta en HDInsight de Azure sin necesidad de volver a crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="2a902-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2a902-127">Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior.</span><span class="sxs-lookup"><span data-stu-id="2a902-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="2a902-128">Si no está seguro de la versión del clúster, puede comprobar la página de propiedades.</span><span class="sxs-lookup"><span data-stu-id="2a902-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="2a902-129">Vea [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="2a902-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="2a902-130">A continuación se muestra el efecto que tiene cambiar la cantidad de nodos de datos de cada tipo de clúster compatible con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2a902-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="2a902-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="2a902-131">Hadoop</span></span>

    <span data-ttu-id="2a902-132">Puede aumentar sin ningún problema la cantidad de nodos de trabajo en un clúster de Hadoop que se encuentre en ejecución, sin que afecte a ningún trabajo pendiente o en ejecución.</span><span class="sxs-lookup"><span data-stu-id="2a902-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="2a902-133">También se pueden enviar trabajos nuevos mientras la operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="2a902-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="2a902-134">Los errores que puedan surgir en una operación de escalado se enfrentan oportunamente, por lo que el clúster siempre queda en estado funcional.</span><span class="sxs-lookup"><span data-stu-id="2a902-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="2a902-135">Cuando se realiza la reducción vertical de un clúster de Hadoop al disminuir la cantidad de nodos de datos, se reinician algunos de los servicios del clúster.</span><span class="sxs-lookup"><span data-stu-id="2a902-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="2a902-136">Esto provoca que todos los trabajos pendientes y en ejecución fallen al completarse la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="2a902-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="2a902-137">Sin embargo, puede volver a enviar los trabajos una vez finalizada la operación.</span><span class="sxs-lookup"><span data-stu-id="2a902-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="2a902-138">HBase</span><span class="sxs-lookup"><span data-stu-id="2a902-138">HBase</span></span>

    <span data-ttu-id="2a902-139">Puede agregar nodos sin problemas al clúster de HBase mientras se encuentra en ejecución, así como eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="2a902-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="2a902-140">Los servidores regionales se equilibran automáticamente en unos pocos minutos tras completar la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="2a902-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="2a902-141">Sin embargo, puede equilibrar manualmente los servidores regionales iniciando sesión en el nodo principal del clúster y ejecutando los comandos siguientes desde una ventana del símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="2a902-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="2a902-142">Storm</span><span class="sxs-lookup"><span data-stu-id="2a902-142">Storm</span></span>

    <span data-ttu-id="2a902-143">Puede agregar o quitar sin problemas nodos de datos de su clúster de Storm mientras se encuentra en ejecución.</span><span class="sxs-lookup"><span data-stu-id="2a902-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="2a902-144">Sin embargo, después de finalizar correctamente la operación de escalado, deberá volver a equilibrar la topología.</span><span class="sxs-lookup"><span data-stu-id="2a902-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="2a902-145">Esto se puede realizar de dos formas:</span><span class="sxs-lookup"><span data-stu-id="2a902-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="2a902-146">La interfaz de usuario web de Storm</span><span class="sxs-lookup"><span data-stu-id="2a902-146">Storm web UI</span></span>
  * <span data-ttu-id="2a902-147">La herramienta de la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="2a902-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="2a902-148">Consulte la [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="2a902-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="2a902-149">La interfaz de usuario web de Storm se encuentra disponible en el clúster de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2a902-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![reequilibrio de escalado de storm de HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="2a902-151">El siguiente es un ejemplo de cómo usar el comando CLI para volver a equilibrar la topología de Storm:</span><span class="sxs-lookup"><span data-stu-id="2a902-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="2a902-152">Para cambiar el tamaño del clúster de Hadoop con Azure PowerShell, ejecute el siguiente comando desde un equipo cliente:</span><span class="sxs-lookup"><span data-stu-id="2a902-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="2a902-153">Concesión o revocación del acceso</span><span class="sxs-lookup"><span data-stu-id="2a902-153">Grant/revoke access</span></span>
<span data-ttu-id="2a902-154">Los clústeres de HDInsight tienen los siguientes servicios web HTTP (todos estos servicios tienen extremos RESTful):</span><span class="sxs-lookup"><span data-stu-id="2a902-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="2a902-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="2a902-155">ODBC</span></span>
* <span data-ttu-id="2a902-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="2a902-156">JDBC</span></span>
* <span data-ttu-id="2a902-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="2a902-157">Ambari</span></span>
* <span data-ttu-id="2a902-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="2a902-158">Oozie</span></span>
* <span data-ttu-id="2a902-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="2a902-159">Templeton</span></span>

<span data-ttu-id="2a902-160">De manera predeterminada, estos servicios se conceden para el acceso.</span><span class="sxs-lookup"><span data-stu-id="2a902-160">By default, these services are granted for access.</span></span> <span data-ttu-id="2a902-161">Puede revocar/conceder el acceso.</span><span class="sxs-lookup"><span data-stu-id="2a902-161">You can revoke/grant the access.</span></span> <span data-ttu-id="2a902-162">Para revocar:</span><span class="sxs-lookup"><span data-stu-id="2a902-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="2a902-163">Para conceder:</span><span class="sxs-lookup"><span data-stu-id="2a902-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="2a902-164">Al conceder/revocar el acceso, restablecerá el nombre de usuario y la contraseña del clúster.</span><span class="sxs-lookup"><span data-stu-id="2a902-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="2a902-165">Esto también se puede hacer a través del Portal.</span><span class="sxs-lookup"><span data-stu-id="2a902-165">This can also be done via the Portal.</span></span> <span data-ttu-id="2a902-166">Consulte [Administración de HDInsight mediante Azure Portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="2a902-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="2a902-167">Actualización de las credenciales de usuario HTTP</span><span class="sxs-lookup"><span data-stu-id="2a902-167">Update HTTP user credentials</span></span>
<span data-ttu-id="2a902-168">Es el mismo procedimiento que [Concesión o revocación del acceso HTTP](#grant/revoke-access). Si al clúster se le ha concedido el acceso HTTP, primero debe revocarlo.</span><span class="sxs-lookup"><span data-stu-id="2a902-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="2a902-169">Y después conceda el acceso con nuevas credenciales de usuario HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a902-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="2a902-170">Búsqueda de la cuenta de almacenamiento predeterminada</span><span class="sxs-lookup"><span data-stu-id="2a902-170">Find the default storage account</span></span>
<span data-ttu-id="2a902-171">El siguiente script de Powershell muestra cómo obtener el nombre y la clave de la cuenta de almacenamiento predeterminada  para un clúster.</span><span class="sxs-lookup"><span data-stu-id="2a902-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="2a902-172">Búsqueda del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2a902-172">Find the resource group</span></span>
<span data-ttu-id="2a902-173">En el modo de Resource Manager, cada clúster de HDInsight pertenece a un grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2a902-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="2a902-174">Para buscar el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="2a902-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="2a902-175">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="2a902-175">Submit jobs</span></span>
<span data-ttu-id="2a902-176">**Para enviar trabajos de MapReduce**</span><span class="sxs-lookup"><span data-stu-id="2a902-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="2a902-177">Vea [Ejecución de ejemplos de Hadoop MapReduce en HDInsight basado en Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2a902-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="2a902-178">**Para enviar trabajos de Hive**</span><span class="sxs-lookup"><span data-stu-id="2a902-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="2a902-179">Vea [Ejecución de consultas de Hive con PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2a902-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="2a902-180">**Para enviar trabajos de Pigs**</span><span class="sxs-lookup"><span data-stu-id="2a902-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="2a902-181">Vea [Ejecución de trabajos de Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2a902-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="2a902-182">**Para enviar trabajos de Sqoop**</span><span class="sxs-lookup"><span data-stu-id="2a902-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="2a902-183">Consulte [Uso de Sqoop con HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="2a902-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="2a902-184">**Para enviar trabajos de Oozie**</span><span class="sxs-lookup"><span data-stu-id="2a902-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="2a902-185">Vea [Uso de Oozie con Hadoop para definir y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="2a902-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="2a902-186">Carga de archivos de datos al almacenamiento de blobs de Azure</span><span class="sxs-lookup"><span data-stu-id="2a902-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="2a902-187">Consulte [Carga de datos en HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="2a902-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="2a902-188">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="2a902-188">See Also</span></span>
* <span data-ttu-id="2a902-189">[Documentación de referencia de los cmdlets de HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="2a902-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="2a902-190">[Administración de HDInsight mediante Azure Portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="2a902-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="2a902-191">[Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="2a902-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="2a902-192">[Creación de clústeres de HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="2a902-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="2a902-193">[Carga de datos en HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="2a902-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="2a902-194">[Envío de trabajos de Hadoop mediante programación][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="2a902-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="2a902-195">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="2a902-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
