---
title: "Personalización de los clústeres de HDInsight con Bootstrap - Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo personalizar clústeres de HDInsight con bootstrap."
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
ms.openlocfilehash: c7a6fafa90eac66774d564c82c926c662baf784c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="8ead0-103">Personalización de los clústeres de HDInsight con Bootstrap</span><span class="sxs-lookup"><span data-stu-id="8ead0-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="8ead0-104">Es probable que en ocasiones desee establecer los valores de archivos de configuración, que incluyen lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ead0-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="8ead0-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="8ead0-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-106">core-site.xml</span></span>
* <span data-ttu-id="8ead0-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-107">gateway.xml</span></span>
* <span data-ttu-id="8ead0-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-108">hbase-env.xml</span></span>
* <span data-ttu-id="8ead0-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-109">hbase-site.xml</span></span>
* <span data-ttu-id="8ead0-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-110">hdfs-site.xml</span></span>
* <span data-ttu-id="8ead0-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-111">hive-env.xml</span></span>
* <span data-ttu-id="8ead0-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-112">hive-site.xml</span></span>
* <span data-ttu-id="8ead0-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="8ead0-113">mapred-site</span></span>
* <span data-ttu-id="8ead0-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-114">oozie-site.xml</span></span>
* <span data-ttu-id="8ead0-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-115">oozie-env.xml</span></span>
* <span data-ttu-id="8ead0-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-116">storm-site.xml</span></span>
* <span data-ttu-id="8ead0-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-117">tez-site.xml</span></span>
* <span data-ttu-id="8ead0-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-118">webhcat-site.xml</span></span>
* <span data-ttu-id="8ead0-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="8ead0-119">yarn-site.xml</span></span>

<span data-ttu-id="8ead0-120">Hay tres métodos para usar bootstrap:</span><span class="sxs-lookup"><span data-stu-id="8ead0-120">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="8ead0-121">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ead0-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="8ead0-122">Uso del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="8ead0-122">Use .NET SDK</span></span>
* <span data-ttu-id="8ead0-123">Usar plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ead0-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="8ead0-124">Para obtener información sobre cómo instalar más componentes en el clúster de HDInsight durante la creación, vea:</span><span class="sxs-lookup"><span data-stu-id="8ead0-124">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="8ead0-125">Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)</span><span class="sxs-lookup"><span data-stu-id="8ead0-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="8ead0-126">Uso de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ead0-126">Use Azure PowerShell</span></span>
<span data-ttu-id="8ead0-127">El siguiente código de PowerShell personaliza una configuración de Hive:</span><span class="sxs-lookup"><span data-stu-id="8ead0-127">The following PowerShell code customizes a Hive configuration:</span></span>

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

<span data-ttu-id="8ead0-128">En el [Anexo A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)aparece un script de PowerShell completamente en uso.</span><span class="sxs-lookup"><span data-stu-id="8ead0-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="8ead0-129">**Para comprobar el cambio:**</span><span class="sxs-lookup"><span data-stu-id="8ead0-129">**To verify the change:**</span></span>

1. <span data-ttu-id="8ead0-130">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ead0-130">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8ead0-131">Haga clic en **Clústeres de HDInsight** en el menú de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="8ead0-131">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="8ead0-132">Si no lo ve, haga clic primero en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="8ead0-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="8ead0-133">Haga clic en el clúster que acaba de crear mediante el script de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ead0-133">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="8ead0-134">Haga clic en el **Panel** desde la parte superior de la hoja para abrir la IU de Ambari.</span><span class="sxs-lookup"><span data-stu-id="8ead0-134">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="8ead0-135">Haga clic en **Hive** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="8ead0-135">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="8ead0-136">Haga clic en **HiveServer2** en **Summary** (Resumen).</span><span class="sxs-lookup"><span data-stu-id="8ead0-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="8ead0-137">Seleccione la pestaña **Configs** (Configuraciones).</span><span class="sxs-lookup"><span data-stu-id="8ead0-137">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="8ead0-138">Haga clic en **Hive** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="8ead0-138">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="8ead0-139">Haga clic en la pestaña **Advanced** (Opciones avanzadas).</span><span class="sxs-lookup"><span data-stu-id="8ead0-139">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="8ead0-140">Desplácese hacia abajo y expanda **Advanced hive-site**(Sitio de Hive avanzado).</span><span class="sxs-lookup"><span data-stu-id="8ead0-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="8ead0-141">Busque **hive.metastore.client.socket.timeout** en la sección.</span><span class="sxs-lookup"><span data-stu-id="8ead0-141">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="8ead0-142">Otros ejemplos de cómo personalizar otros archivos de configuración:</span><span class="sxs-lookup"><span data-stu-id="8ead0-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="8ead0-143">Para más información, vea el blog de Azim Uddin titulado [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)(Personalización de la creación de clústeres de HDInsight).</span><span class="sxs-lookup"><span data-stu-id="8ead0-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="8ead0-144">Uso del SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="8ead0-144">Use .NET SDK</span></span>
<span data-ttu-id="8ead0-145">Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span><span class="sxs-lookup"><span data-stu-id="8ead0-145">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="8ead0-146">Uso de plantillas de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ead0-146">Use Resource Manager template</span></span>
<span data-ttu-id="8ead0-147">Puede usar Bootstrap en la plantilla de Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="8ead0-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop personaliza la plantilla de Azure Resource Manager de Bootstrap del clúster](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="8ead0-149">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8ead0-149">See also</span></span>
* <span data-ttu-id="8ead0-150">En [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision-cluster] se proporcionan instrucciones sobre cómo crear un clúster de HDInsight con otras opciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="8ead0-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="8ead0-151">[Desarrollo de acciones de script con HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="8ead0-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="8ead0-152">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="8ead0-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="8ead0-153">[Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="8ead0-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="8ead0-154">[Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="8ead0-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="8ead0-155">[Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="8ead0-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="8ead0-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fases durante la creación del clúster"</span><span class="sxs-lookup"><span data-stu-id="8ead0-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="8ead0-157">Anexo A: ejemplo de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ead0-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="8ead0-158">Este script de PowerShell crea un clúster de HDInsight y personaliza una configuración de Hive:</span><span class="sxs-lookup"><span data-stu-id="8ead0-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

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
    # Connect to Azure
    ####################################
    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

    Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
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
        -Context $defaultStorageContext #use the cluster name as the container name

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
    # Verify the cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
