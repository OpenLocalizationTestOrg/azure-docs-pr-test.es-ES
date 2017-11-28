---
title: "clústeres de aaaManage Hadoop en HDInsight con PowerShell, Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooperform administrativa tareas para hello clústeres de Hadoop en HDInsight con Azure PowerShell."
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
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="399da-103">Administración de clústeres de Hadoop en HDInsight con PowerShell de Azure</span><span class="sxs-lookup"><span data-stu-id="399da-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="399da-104">Azure PowerShell es un entorno de scripting eficaz que puede usar toocontrol y automatizar la implementación de Hola y administración de las cargas de trabajo en Azure.</span><span class="sxs-lookup"><span data-stu-id="399da-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="399da-105">En este artículo, aprenderá cómo toomanage clústeres de Hadoop en HDInsight de Azure mediante una consola de PowerShell de Azure local a través de hello el uso de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="399da-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="399da-106">Para lista de Hola de hello HDInsight PowerShell cmdlets, consulte [referencia de cmdlets de HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="399da-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="399da-107">**Requisitos previos**</span><span class="sxs-lookup"><span data-stu-id="399da-107">**Prerequisites**</span></span>

<span data-ttu-id="399da-108">Antes de comenzar este artículo, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="399da-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="399da-109">**Una suscripción de Azure**.</span><span class="sxs-lookup"><span data-stu-id="399da-109">**An Azure subscription**.</span></span> <span data-ttu-id="399da-110">Consulte [Obtención de una versión de evaluación gratuita](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="399da-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="399da-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="399da-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="399da-112">Si ha instalado la versión 0.9 x de Azure PowerShell, debe desinstalarla antes de instalar una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="399da-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="399da-113">versión de hello toocheck de hello había instalado PowerShell:</span><span class="sxs-lookup"><span data-stu-id="399da-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="399da-114">toouninstall Hola versión anterior, ejecutar programas y características en el panel de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="399da-115">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="399da-115">Create clusters</span></span>
<span data-ttu-id="399da-116">Consulte [Crear clústeres basados en Linux en HDInsight con Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="399da-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="399da-117">Enumeración de clústeres</span><span class="sxs-lookup"><span data-stu-id="399da-117">List clusters</span></span>
<span data-ttu-id="399da-118">Usar hello después a toolist comando todos los clústeres en la suscripción actual de hello:</span><span class="sxs-lookup"><span data-stu-id="399da-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="399da-119">Presentación de clústeres</span><span class="sxs-lookup"><span data-stu-id="399da-119">Show cluster</span></span>
<span data-ttu-id="399da-120">Usar hello comando tooshow detalles de un clúster concreto en la suscripción actual de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="399da-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="399da-121">Eliminación de clústeres</span><span class="sxs-lookup"><span data-stu-id="399da-121">Delete clusters</span></span>
<span data-ttu-id="399da-122">Usar hello después comando toodelete un clúster:</span><span class="sxs-lookup"><span data-stu-id="399da-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="399da-123">También puede eliminar un clúster mediante la eliminación de grupo de recursos de Hola que contiene el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="399da-124">Tenga en cuenta, se eliminarán todos los recursos de hello en grupo de hello incluidas cuenta de almacenamiento predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="399da-125">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="399da-125">Scale clusters</span></span>
<span data-ttu-id="399da-126">característica de ajuste de escala de clúster de Hola permite toochange número de Hola de nodos de trabajador usado por un clúster que se ejecuta en HDInsight de Azure sin necesidad de toore-crear clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="399da-127">Solo son compatibles los clústeres con la versión 3.1.3 de HDInsight, o superior.</span><span class="sxs-lookup"><span data-stu-id="399da-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="399da-128">Si no está seguro de la versión de Hola del clúster, puede comprobar la página de propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="399da-129">Consulte [Enumeración y visualización de clústeres](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="399da-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="399da-130">impacto de Hola de cambiar el número de Hola de nodos de datos para cada tipo de clúster compatible con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="399da-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="399da-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="399da-131">Hadoop</span></span>

    <span data-ttu-id="399da-132">Perfectamente puede aumentar el número de Hola de nodos de trabajador en un clúster de Hadoop que se ejecuta sin afectar a los trabajos pendientes o en ejecución.</span><span class="sxs-lookup"><span data-stu-id="399da-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="399da-133">También se pueden enviar trabajos nuevos mientras Hola operación está en curso.</span><span class="sxs-lookup"><span data-stu-id="399da-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="399da-134">Errores en una operación de ajuste de escala se controlan correctamente para que hello clúster siempre se deja en un estado funcional.</span><span class="sxs-lookup"><span data-stu-id="399da-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="399da-135">Cuando un clúster de Hadoop es reducido reduciendo el número de Hola de nodos de datos, algunos de los servicios de hello en clúster de Hola se reinician.</span><span class="sxs-lookup"><span data-stu-id="399da-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="399da-136">Esto hace que ejecutan todos y pendiente de trabajos toofail al término de Hola Hola la operación de escalado.</span><span class="sxs-lookup"><span data-stu-id="399da-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="399da-137">Sin embargo, puede volver a enviar trabajos de hello una vez completada la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="399da-138">HBase</span><span class="sxs-lookup"><span data-stu-id="399da-138">HBase</span></span>

    <span data-ttu-id="399da-139">Sin problemas, puede agregar o quitar el clúster de HBase tooyour nodos mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="399da-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="399da-140">Los servidores regionales se equilibran automáticamente dentro de unos pocos minutos después de completar la operación de escalado de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="399da-141">No obstante, puede equilibrar manualmente servidores regionales Hola al iniciar sesión en el nodo principal de toohello del clúster y ejecución Hola siguientes comandos de una ventana del símbolo del sistema:</span><span class="sxs-lookup"><span data-stu-id="399da-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="399da-142">Storm</span><span class="sxs-lookup"><span data-stu-id="399da-142">Storm</span></span>

    <span data-ttu-id="399da-143">Sin problemas, puede agregar o quitar el clúster de Storm de tooyour de nodos de datos mientras se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="399da-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="399da-144">Sin embargo, tras finalizar correctamente la operación de escalado de hello, debe topología de hello toorebalance.</span><span class="sxs-lookup"><span data-stu-id="399da-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="399da-145">Esto se puede realizar de dos formas:</span><span class="sxs-lookup"><span data-stu-id="399da-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="399da-146">La interfaz de usuario web de Storm</span><span class="sxs-lookup"><span data-stu-id="399da-146">Storm web UI</span></span>
  * <span data-ttu-id="399da-147">La herramienta de la interfaz de línea de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="399da-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="399da-148">Consulte toohello [documentación de Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="399da-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="399da-149">interfaz de usuario de web de Storm Hola está disponible en el clúster de HDInsight de hello:</span><span class="sxs-lookup"><span data-stu-id="399da-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![reequilibrio de escalado de storm de HDInsight](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="399da-151">Este es un ejemplo cómo toouse Hola CLI comando topología de Storm Hola toorebalance:</span><span class="sxs-lookup"><span data-stu-id="399da-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="399da-152">Hola toochange tamaño de clúster de Hadoop mediante Azure PowerShell, ejecute hello siguiente comando desde un equipo cliente:</span><span class="sxs-lookup"><span data-stu-id="399da-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="399da-153">Concesión o revocación del acceso</span><span class="sxs-lookup"><span data-stu-id="399da-153">Grant/revoke access</span></span>
<span data-ttu-id="399da-154">Clústeres de HDInsight tienen Hola después de servicios web HTTP (todos estos servicios tienen extremos RESTful):</span><span class="sxs-lookup"><span data-stu-id="399da-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="399da-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="399da-155">ODBC</span></span>
* <span data-ttu-id="399da-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="399da-156">JDBC</span></span>
* <span data-ttu-id="399da-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="399da-157">Ambari</span></span>
* <span data-ttu-id="399da-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="399da-158">Oozie</span></span>
* <span data-ttu-id="399da-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="399da-159">Templeton</span></span>

<span data-ttu-id="399da-160">De manera predeterminada, estos servicios se conceden para el acceso.</span><span class="sxs-lookup"><span data-stu-id="399da-160">By default, these services are granted for access.</span></span> <span data-ttu-id="399da-161">Puede revocar y conceder acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="399da-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="399da-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="399da-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="399da-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="399da-164">Por conceder o revocar el acceso de hello, se restablecerá la contraseña y el nombre de usuario del clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="399da-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="399da-165">Esto puede hacerse a través de hello Portal.</span><span class="sxs-lookup"><span data-stu-id="399da-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="399da-166">Vea [HDInsight administrar mediante el uso de Hola portal de Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="399da-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="399da-167">Actualización de las credenciales de usuario HTTP</span><span class="sxs-lookup"><span data-stu-id="399da-167">Update HTTP user credentials</span></span>
<span data-ttu-id="399da-168">Es Hola mismo procedimiento como [HTTP conceder o revocar acceso](#grant/revoke-access). Si se concedió clúster Hola Hola acceso HTTP, debe revocar primero.</span><span class="sxs-lookup"><span data-stu-id="399da-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="399da-169">Y, a continuación, conceder acceso de hello con nuevas credenciales de usuario HTTP.</span><span class="sxs-lookup"><span data-stu-id="399da-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="399da-170">Busque la cuenta de almacenamiento predeterminada de Hola</span><span class="sxs-lookup"><span data-stu-id="399da-170">Find hello default storage account</span></span>
<span data-ttu-id="399da-171">Hola siguiente script de Powershell muestra cómo tooget nombre de cuenta de almacenamiento predeterminado de Hola y Hola clave de cuenta de almacenamiento predeterminada para un clúster.</span><span class="sxs-lookup"><span data-stu-id="399da-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="399da-172">Encontrar el grupo de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="399da-172">Find hello resource group</span></span>
<span data-ttu-id="399da-173">En el modo de administrador de recursos de hello, cada clúster de HDInsight pertenece tooan grupo de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="399da-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="399da-174">grupo de recursos de Hola toofind:</span><span class="sxs-lookup"><span data-stu-id="399da-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="399da-175">Envío de trabajos</span><span class="sxs-lookup"><span data-stu-id="399da-175">Submit jobs</span></span>
<span data-ttu-id="399da-176">**trabajos de MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="399da-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="399da-177">Vea [Ejecución de ejemplos de Hadoop MapReduce en HDInsight basado en Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="399da-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="399da-178">**trabajos de Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="399da-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="399da-179">Vea [Ejecución de consultas de Hive con PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="399da-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="399da-180">**trabajos de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="399da-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="399da-181">Vea [Ejecución de trabajos de Pig mediante PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="399da-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="399da-182">**trabajos de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="399da-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="399da-183">Consulte [Uso de Sqoop con HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="399da-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="399da-184">**trabajos de Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="399da-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="399da-185">Vea [Oozie de uso con Hadoop toodefine y ejecutar un flujo de trabajo en HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="399da-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="399da-186">Cargar el almacenamiento de blobs de datos tooAzure</span><span class="sxs-lookup"><span data-stu-id="399da-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="399da-187">Vea [cargar datos tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="399da-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="399da-188">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="399da-188">See Also</span></span>
* <span data-ttu-id="399da-189">[Documentación de referencia de los cmdlets de HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="399da-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="399da-190">[Administrar HDInsight mediante Hola portal de Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="399da-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="399da-191">[Administración de HDInsight con la interfaz de la línea de comandos][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="399da-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="399da-192">[Creación de clústeres de HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="399da-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="399da-193">[Cargar datos tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="399da-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="399da-194">[Envío de trabajos de Hadoop mediante programación][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="399da-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="399da-195">[Introducción a Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="399da-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
