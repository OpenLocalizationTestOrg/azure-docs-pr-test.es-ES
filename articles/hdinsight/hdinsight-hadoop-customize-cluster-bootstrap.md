---
title: "Clústeres de HDInsight con arranque: Azure aaaCustomize | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize HDInsight clústeres utilizando el arranque."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 0029680fd1aa0e9e6aa9cdf667256c31b7ddc565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="1bf62-103">Personalización de los clústeres de HDInsight con Bootstrap</span><span class="sxs-lookup"><span data-stu-id="1bf62-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="1bf62-104">A veces, desea que los archivos de configuración de tooconfigure hello, que incluyen:</span><span class="sxs-lookup"><span data-stu-id="1bf62-104">Sometimes, you want tooconfigure hello configuration files, which include:</span></span>

* <span data-ttu-id="1bf62-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="1bf62-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-106">core-site.xml</span></span>
* <span data-ttu-id="1bf62-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-107">gateway.xml</span></span>
* <span data-ttu-id="1bf62-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-108">hbase-env.xml</span></span>
* <span data-ttu-id="1bf62-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-109">hbase-site.xml</span></span>
* <span data-ttu-id="1bf62-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-110">hdfs-site.xml</span></span>
* <span data-ttu-id="1bf62-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-111">hive-env.xml</span></span>
* <span data-ttu-id="1bf62-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-112">hive-site.xml</span></span>
* <span data-ttu-id="1bf62-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="1bf62-113">mapred-site</span></span>
* <span data-ttu-id="1bf62-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-114">oozie-site.xml</span></span>
* <span data-ttu-id="1bf62-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-115">oozie-env.xml</span></span>
* <span data-ttu-id="1bf62-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-116">storm-site.xml</span></span>
* <span data-ttu-id="1bf62-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-117">tez-site.xml</span></span>
* <span data-ttu-id="1bf62-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-118">webhcat-site.xml</span></span>
* <span data-ttu-id="1bf62-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="1bf62-119">yarn-site.xml</span></span>

<span data-ttu-id="1bf62-120">Hay tres toouse métodos arranque:</span><span class="sxs-lookup"><span data-stu-id="1bf62-120">There are three methods toouse bootstrap:</span></span>

* <span data-ttu-id="1bf62-121">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bf62-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="1bf62-122">Uso del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="1bf62-122">Use .NET SDK</span></span>
* <span data-ttu-id="1bf62-123">Usar plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1bf62-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="1bf62-124">Para obtener información acerca de cómo instalar componentes adicionales en el clúster de HDInsight durante el tiempo de creación de hello, vea:</span><span class="sxs-lookup"><span data-stu-id="1bf62-124">For information on installing additional components on HDInsight cluster during hello creation time, see:</span></span>

* [<span data-ttu-id="1bf62-125">Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)</span><span class="sxs-lookup"><span data-stu-id="1bf62-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="1bf62-126">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bf62-126">Use Azure PowerShell</span></span>
<span data-ttu-id="1bf62-127">Hola siguiente código de PowerShell personaliza una configuración de Hive:</span><span class="sxs-lookup"><span data-stu-id="1bf62-127">hello following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="1bf62-128">En el [Anexo A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)aparece un script de PowerShell completamente en uso.</span><span class="sxs-lookup"><span data-stu-id="1bf62-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="1bf62-129">**cambio de Hola tooverify:**</span><span class="sxs-lookup"><span data-stu-id="1bf62-129">**tooverify hello change:**</span></span>

1. <span data-ttu-id="1bf62-130">Inicio de sesión toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1bf62-130">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1bf62-131">Hola menú izquierdo, haga clic en **clústeres de HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1bf62-131">From hello left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="1bf62-132">Si no lo ve, haga clic primero en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="1bf62-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="1bf62-133">Haga clic en el clúster de Hola que acaba de crear mediante script de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf62-133">Click hello cluster you just created using hello PowerShell script.</span></span>
4. <span data-ttu-id="1bf62-134">Haga clic en **panel** de arriba Hola de hello hoja tooopen Hola Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="1bf62-134">Click **Dashboard** from hello top of hello blade tooopen hello Ambari UI.</span></span>
5. <span data-ttu-id="1bf62-135">Haga clic en **Hive** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf62-135">Click **Hive** from hello left menu.</span></span>
6. <span data-ttu-id="1bf62-136">Haga clic en **HiveServer2** en **Summary** (Resumen).</span><span class="sxs-lookup"><span data-stu-id="1bf62-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="1bf62-137">Haga clic en hello **configuraciones** ficha.</span><span class="sxs-lookup"><span data-stu-id="1bf62-137">Click hello **Configs** tab.</span></span>
8. <span data-ttu-id="1bf62-138">Haga clic en **Hive** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf62-138">Click **Hive** from hello left menu.</span></span>
9. <span data-ttu-id="1bf62-139">Haga clic en hello **avanzadas** ficha.</span><span class="sxs-lookup"><span data-stu-id="1bf62-139">Click hello **Advanced** tab.</span></span>
10. <span data-ttu-id="1bf62-140">Desplácese hacia abajo y expanda **Advanced hive-site**(Sitio de Hive avanzado).</span><span class="sxs-lookup"><span data-stu-id="1bf62-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="1bf62-141">Busque **hive.metastore.client.socket.timeout** en la sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="1bf62-141">Look for **hive.metastore.client.socket.timeout** in hello section.</span></span>

<span data-ttu-id="1bf62-142">Otros ejemplos de cómo personalizar otros archivos de configuración:</span><span class="sxs-lookup"><span data-stu-id="1bf62-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="1bf62-143">Para más información, vea el blog de Azim Uddin titulado [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)(Personalización de la creación de clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="1bf62-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="1bf62-144">Uso del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="1bf62-144">Use .NET SDK</span></span>
<span data-ttu-id="1bf62-145">Vea [basados en Linux crear clústeres de HDInsight utilizando Hola .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="1bf62-145">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="1bf62-146">Uso de plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1bf62-146">Use Resource Manager template</span></span>
<span data-ttu-id="1bf62-147">Puede usar Bootstrap en la plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="1bf62-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personaliza la plantilla de Azure Resource Manager de Bootstrap del clúster](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="1bf62-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="1bf62-149">See also</span></span>
* <span data-ttu-id="1bf62-150">[Crear clústeres de Hadoop en HDInsight] [ hdinsight-provision-cluster] proporciona instrucciones sobre cómo toocreate una HDInsight de clúster mediante el uso de otras opciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1bf62-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="1bf62-151">[Desarrollo de acciones de script con HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="1bf62-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="1bf62-152">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="1bf62-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="1bf62-153">[Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="1bf62-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="1bf62-154">[Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="1bf62-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="1bf62-155">[Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="1bf62-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fases durante la creación del clúster"

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="1bf62-157">Anexo A: ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bf62-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="1bf62-158">Este script de PowerShell crea un clúster de HDInsight y personaliza una configuración de Hive:</span><span class="sxs-lookup"><span data-stu-id="1bf62-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect tooAzure
    ####################################
    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating hello default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use hello cluster name as hello container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify hello cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
