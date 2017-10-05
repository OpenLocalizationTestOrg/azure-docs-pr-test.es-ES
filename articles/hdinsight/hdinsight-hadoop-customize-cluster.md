---
title: "Personalización de clústeres de HDInsight mediante acciones de script - Azure | Microsoft Docs"
description: "Obtenga información acerca de cómo personalizar clústeres de HDInsight mediante la acción de script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="4d85c-103">Personalización de clústeres de HDInsight mediante la acción de scripts (Windows)</span><span class="sxs-lookup"><span data-stu-id="4d85c-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="4d85c-104">**acción de script** se puede usar para invocar [scripts personalizados](hdinsight-hadoop-script-actions.md) durante el proceso de creación de clústeres para instalar software adicional en un clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="4d85c-105">La información de este artículo es específica de los clústeres de HDInsight basados en Windows.</span><span class="sxs-lookup"><span data-stu-id="4d85c-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4d85c-106">Para obtener más información sobre clústeres basados en Linux, vea [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d85c-107">Linux es el único sistema operativo que se usa en la versión 3.4 de HDInsight, o en las superiores.</span><span class="sxs-lookup"><span data-stu-id="4d85c-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4d85c-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4d85c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="4d85c-109">Los clústeres de HDInsight se pueden personalizar de muchas maneras distintas, por ejemplo, con la inclusión de cuentas de almacenamiento de Azure adicionales, mediante el cambio de archivos de configuración de Hadoop (core-site.xml, hive-site.xml, etc.) o mediante la adición de bibliotecas compartidas (por ejemplo, Oozie o Hive) en ubicaciones comunes en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="4d85c-110">Estas personalizaciones pueden realizarse a través de Azure PowerShell, el SDK para .NET de HDInsight de Azure o Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d85c-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="4d85c-111">Para obtener más información, consulte [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="4d85c-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="4d85c-112">Acción de script en el proceso de aprovisionamiento de clústeres</span><span class="sxs-lookup"><span data-stu-id="4d85c-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="4d85c-113">Acción de script solo se utiliza mientras un clúster está en proceso de creación.</span><span class="sxs-lookup"><span data-stu-id="4d85c-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="4d85c-114">El siguiente diagrama ilustra el momento en que acción de script se ejecuta durante el proceso de aprovisionamiento:</span><span class="sxs-lookup"><span data-stu-id="4d85c-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="4d85c-115">![Fases y personalización de clústeres de HDInsight durante la creación de clústeres][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="4d85c-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="4d85c-116">Cuando se ejecuta el script, el clúster entra en la fase **ClusterCustomization**.</span><span class="sxs-lookup"><span data-stu-id="4d85c-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="4d85c-117">En esta fase, el script se ejecuta bajo la cuenta de administrador del sistema, de forma paralela a todos los nodos especificados en el clúster. Asimismo, proporciona privilegios completos de administrador en los nodos.</span><span class="sxs-lookup"><span data-stu-id="4d85c-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="4d85c-118">Puesto que dispone de privilegios de administrador en los nodos del clúster durante la fase **ClusterCustomization** , podrá usar el script para realizar operaciones como la detención o el inicio de servicios, incluidos los servicios de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4d85c-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="4d85c-119">Por lo tanto, como parte del script, debe asegurarse de que los servicios de Ambari y los demás servicios de Hadoop estén en funcionamiento antes de que finalice el script.</span><span class="sxs-lookup"><span data-stu-id="4d85c-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="4d85c-120">Estos servicios son necesarios para determinar correctamente el estado del clúster durante la creación.</span><span class="sxs-lookup"><span data-stu-id="4d85c-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="4d85c-121">Si modifica cualquier configuración en el clúster que afecte a estos servicios, deberá usar las funciones auxiliares proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="4d85c-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="4d85c-122">Para obtener más información sobre las funciones auxiliares, consulte [Desarrollo de la acción de script con HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="4d85c-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="4d85c-123">Los registros de errores y resultados del script se almacenan en la cuenta de almacenamiento predeterminada especificada para el clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="4d85c-124">Los registros se almacenan en una tabla con el nombre **u<\cluster-name-fragment><\time-stamp>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="4d85c-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="4d85c-125">Estos son registros agregados desde la ejecución del script en todos los nodos (nodos principal y de trabajo) del clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="4d85c-126">Cada clúster puede aceptar varias acciones de script, que se invocan en el orden en que se hayan especificado.</span><span class="sxs-lookup"><span data-stu-id="4d85c-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="4d85c-127">Los scripts se pueden ejecutar en el nodo principal, los nodos de trabajo, o ambos.</span><span class="sxs-lookup"><span data-stu-id="4d85c-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="4d85c-128">HDInsight proporciona varios scripts para instalar los siguientes componentes en clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4d85c-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="4d85c-129">Nombre</span><span class="sxs-lookup"><span data-stu-id="4d85c-129">Name</span></span> | <span data-ttu-id="4d85c-130">Script</span><span class="sxs-lookup"><span data-stu-id="4d85c-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="4d85c-131">**Instalar Spark**</span><span class="sxs-lookup"><span data-stu-id="4d85c-131">**Install Spark**</span></span> |<span data-ttu-id="4d85c-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="4d85c-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="4d85c-133">Vea [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="4d85c-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="4d85c-134">**Instalar R**</span><span class="sxs-lookup"><span data-stu-id="4d85c-134">**Install R**</span></span> |<span data-ttu-id="4d85c-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="4d85c-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="4d85c-136">Consulte [Instalación y uso de R en clústeres de HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="4d85c-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="4d85c-137">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="4d85c-137">**Install Solr**</span></span> |<span data-ttu-id="4d85c-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="4d85c-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="4d85c-139">Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="4d85c-140">- **Instalar Giraph**</span><span class="sxs-lookup"><span data-stu-id="4d85c-140">- **Install Giraph**</span></span> |<span data-ttu-id="4d85c-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="4d85c-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="4d85c-142">Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="4d85c-143">**Carga previa de las bibliotecas de Hive**</span><span class="sxs-lookup"><span data-stu-id="4d85c-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="4d85c-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="4d85c-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="4d85c-145">Vea [Incorporación de bibliotecas de Hive durante la creación de clústeres de HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="4d85c-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="4d85c-146">Llamada a scripts con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4d85c-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="4d85c-147">**En Azure portal**</span><span class="sxs-lookup"><span data-stu-id="4d85c-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="4d85c-148">Comience a crear un clúster, tal y como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="4d85c-149">En Configuración opcional de la hoja **Acciones de script**, haga clic en **Agregar acción de script** para proporcionar detalles sobre la acción de script, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="4d85c-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="4d85c-150">![Uso de la acción de script para personalizar un clúster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Uso de la acción de script para personalizar un clúster")</span><span class="sxs-lookup"><span data-stu-id="4d85c-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="4d85c-151">Propiedad</span><span class="sxs-lookup"><span data-stu-id="4d85c-151">Property</span></span></th><th><span data-ttu-id="4d85c-152">Valor</span><span class="sxs-lookup"><span data-stu-id="4d85c-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="4d85c-153">Nombre</span><span class="sxs-lookup"><span data-stu-id="4d85c-153">Name</span></span></td>
            <td><span data-ttu-id="4d85c-154">Especifique un nombre para la acción de script.</span><span class="sxs-lookup"><span data-stu-id="4d85c-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="4d85c-155">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="4d85c-155">Script URI</span></span></td>
            <td><span data-ttu-id="4d85c-156">Especifique el identificador URI al script que se ha invocado para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="4d85c-157">s</span><span class="sxs-lookup"><span data-stu-id="4d85c-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="4d85c-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="4d85c-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="4d85c-159">Especifique los nodos (**Head** o **Worker**) en los que se ejecuta el script de personalización</b>.</span><span class="sxs-lookup"><span data-stu-id="4d85c-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="4d85c-160">Parámetros</span><span class="sxs-lookup"><span data-stu-id="4d85c-160">Parameters</span></span></td>
            <td><span data-ttu-id="4d85c-161">Especifique los parámetros, si lo requiere el script.</span><span class="sxs-lookup"><span data-stu-id="4d85c-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="4d85c-162">Presione ENTRAR para agregar más de una acción de script para instalar varios componentes en el clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="4d85c-163">Haga clic en **Seleccionar** para guardar la configuración de la acción de script y continúe con la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="4d85c-164">Llamada a scripts con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d85c-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="4d85c-165">Este script de PowerShell muestra cómo instalar Spark en un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="4d85c-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="4d85c-166">Para instalar otro software, deberá reemplazar el archivo de script en el script:</span><span class="sxs-lookup"><span data-stu-id="4d85c-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="4d85c-167">Cuando el sistema lo pida, escriba las credenciales para el clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="4d85c-168">El clúster puede tardar varios minutos en crearse.</span><span class="sxs-lookup"><span data-stu-id="4d85c-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="4d85c-169">Llamada a scripts mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4d85c-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="4d85c-170">En el ejemplo siguiente se muestra cómo instalar Spark en un clúster de HDInsight basado en Windows.</span><span class="sxs-lookup"><span data-stu-id="4d85c-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="4d85c-171">Para instalar otro software, deberá reemplazar el archivo de script en el código.</span><span class="sxs-lookup"><span data-stu-id="4d85c-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="4d85c-172">**Para crear un clúster de HDInsight con Spark**</span><span class="sxs-lookup"><span data-stu-id="4d85c-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="4d85c-173">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4d85c-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="4d85c-174">En la Consola del administrador de paquetes Nuget, ejecute el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="4d85c-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="4d85c-175">Use las siguientes instrucciones using en el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="4d85c-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="4d85c-176">Coloque el código de la clase con lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d85c-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="4d85c-177">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d85c-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="4d85c-178">Soporte técnico para el software de código abierto utilizado en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d85c-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="4d85c-179">El servicio HDInsight de Microsoft Azure es una plataforma flexible que permite compilar aplicaciones con grandes volúmenes de datos en la nube mediante el ecosistema de tecnologías de código abierto formadas en torno a Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4d85c-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="4d85c-180">Microsoft Azure ofrece un nivel general de soporte técnico para las tecnologías de código abierto, tal como se describe en la sección **Ámbito de soporte técnico** del <a href="http://azure.microsoft.com/support/faq/" target="_blank">sitio web de Preguntas más frecuentes de soporte técnico de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="4d85c-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="4d85c-181">Además, el servicio de HDInsight ofrece un nivel adicional de soporte técnico para algunos de los componentes, como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="4d85c-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="4d85c-182">Hay dos tipos de componentes de código abierto que están disponibles en el servicio de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4d85c-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="4d85c-183">**Componentes integrados** : estos componentes están instalados previamente en clústeres de HDInsight y proporcionan la funcionalidad básica del clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="4d85c-184">Por ejemplo, el administrador de recursos de YARN, el lenguaje de consulta Hive (HiveQL) y la biblioteca Mahout pertenecen a esta categoría.</span><span class="sxs-lookup"><span data-stu-id="4d85c-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="4d85c-185">Hay una lista completa de los componentes del clúster disponible en [Novedades en las versiones de clústeres de Hadoop proporcionadas por HDInsight](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="4d85c-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="4d85c-186">**Componentes personalizados** : el usuario del clúster puede instalar o usar en la carga de trabajo cualquier componente que esté disponible en la comunidad o que haya creado personalmente.</span><span class="sxs-lookup"><span data-stu-id="4d85c-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="4d85c-187">Los componentes integrados son totalmente compatibles, y el soporte técnico de Microsoft le ayudará a aislar y resolver problemas relacionados con estos componentes.</span><span class="sxs-lookup"><span data-stu-id="4d85c-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="4d85c-188">Los componentes ofrecidos con HDInsight son totalmente compatibles. Además, el soporte técnico de Microsoft le ayudará a aislar y resolver problemas relacionados con estos componentes.</span><span class="sxs-lookup"><span data-stu-id="4d85c-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="4d85c-189">Los componentes personalizados reciben soporte técnico comercialmente razonable para ayudarle a solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="4d85c-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="4d85c-190">Esto podría resolver el problema o pedirle que forme parte de los canales disponibles para las tecnologías de código abierto donde se encuentra la más amplia experiencia para esa tecnología.</span><span class="sxs-lookup"><span data-stu-id="4d85c-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="4d85c-191">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="4d85c-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="4d85c-192">Además, los proyectos de Apache tienen sitios del proyecto en [http://apache.org](http://apache.org), por ejemplo, [Hadoop](http://hadoop.apache.org/) y [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="4d85c-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="4d85c-193">El servicio HDInsight proporciona varias maneras de utilizar los componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="4d85c-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="4d85c-194">Independientemente de cómo se use el componente o cómo se instale en el clúster, se aplica el mismo nivel de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4d85c-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="4d85c-195">A continuación, se muestra una lista de las maneras más comunes que se pueden usar los componentes personalizados en los clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4d85c-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="4d85c-196">Envío de trabajos: se pueden enviar al clúster trabajos de Hadoop o de otros tipos que ejecuten o usen componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="4d85c-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="4d85c-197">Personalización del clúster: durante la creación del clúster puede especificar una configuración adicional y componentes personalizados que se instalarán en los nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="4d85c-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="4d85c-198">Muestras: para los componentes personalizados más populares, Microsoft y otros pueden proporcionar muestras de cómo estos componentes se pueden utilizar en los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4d85c-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="4d85c-199">Estas muestras se proporcionan sin soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="4d85c-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="4d85c-200">Desarrollo de scripts de acción de script</span><span class="sxs-lookup"><span data-stu-id="4d85c-200">Develop Script Action scripts</span></span>
<span data-ttu-id="4d85c-201">Consulte [Desarrollo de scripts de acciones de script con HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="4d85c-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="4d85c-202">Consulte también</span><span class="sxs-lookup"><span data-stu-id="4d85c-202">See also</span></span>
* <span data-ttu-id="4d85c-203">En [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision-cluster] se proporcionan instrucciones sobre cómo crear un clúster de HDInsight con otras opciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="4d85c-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="4d85c-204">[Desarrollo de acciones de script con HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="4d85c-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="4d85c-205">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="4d85c-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="4d85c-206">[Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="4d85c-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="4d85c-207">[Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="4d85c-208">[Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="4d85c-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="4d85c-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fases durante la creación del clúster"</span><span class="sxs-lookup"><span data-stu-id="4d85c-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
