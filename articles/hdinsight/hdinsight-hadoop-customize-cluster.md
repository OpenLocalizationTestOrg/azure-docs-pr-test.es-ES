---
title: "uso de clústeres de HDInsight de aaaCustomize script acciones - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocustomize HDInsight clústeres utilizando la acción de secuencia de comandos."
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
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="fc559-103">Personalización de clústeres de HDInsight mediante la acción de scripts (Windows)</span><span class="sxs-lookup"><span data-stu-id="fc559-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="fc559-104">**Acción de secuencia de comandos** puede ser usado tooinvoke [scripts personalizados](hdinsight-hadoop-script-actions.md) durante el proceso de creación de clúster de Hola para instalar software adicional en un clúster.</span><span class="sxs-lookup"><span data-stu-id="fc559-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="fc559-105">información de Hello en este artículo es específicos clústeres de HDInsight basados en tooWindows.</span><span class="sxs-lookup"><span data-stu-id="fc559-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="fc559-106">Para obtener más información sobre clústeres basados en Linux, vea [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc559-107">Linux es Hola único sistema operativo usado en HDInsight versión 3.4 o superior.</span><span class="sxs-lookup"><span data-stu-id="fc559-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fc559-108">Consulte la información sobre la [retirada de HDInsight en Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fc559-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="fc559-109">Clústeres de HDInsight pueden personalizarse en una variedad de otras maneras, como la inclusión de las cuentas de almacenamiento de Azure adicionales, cambiar hello Hadoop (core-site.xml, hive-site.xml, etc.) de los archivos de configuración o agregar compartidas bibliotecas (p. ej., Hive y Oozie) en ubicaciones comunes en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="fc559-110">Estas personalizaciones pueden hacerse a través de PowerShell de Azure, hello Azure HDInsight .NET SDK, u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc559-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="fc559-111">Para obtener más información, consulte [Creación de clústeres de Hadoop en HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="fc559-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="fc559-112">Acción de secuencia de comandos en el proceso de creación de clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="fc559-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="fc559-113">Generar script de acción solo se usa cuando un clúster está en proceso de Hola de que se está creando.</span><span class="sxs-lookup"><span data-stu-id="fc559-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="fc559-114">Hello siguiente diagrama se muestra cuando se ejecuta la acción de secuencia de comandos durante el proceso de creación de hello:</span><span class="sxs-lookup"><span data-stu-id="fc559-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="fc559-115">![Fases y personalización de clústeres de HDInsight durante la creación de clústeres][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="fc559-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="fc559-116">Cuando se ejecuta el script de Hola, clúster de hello entra en hello **ClusterCustomization** fase.</span><span class="sxs-lookup"><span data-stu-id="fc559-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="fc559-117">En esta fase, Hola script se ejecuta bajo la cuenta de administrador del sistema de hello, en paralelo en todos los Hola especificado nodos de clúster de Hola y proporciona privilegios de administrador total en nodos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="fc559-118">Dado que tiene privilegios de administrador en los nodos de clúster de Hola durante el **ClusterCustomization** fase, puede utilizar operaciones de tooperform de script de Hola como detener e iniciar servicios, incluidos los servicios relacionados con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fc559-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="fc559-119">Por lo tanto, como parte del script de Hola, debe asegurarse de esa hello Ambari servicios y otros servicios relacionados con Hadoop están activados y ejecutándose antes de que finaliza la ejecución de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="fc559-120">Estos servicios son necesarios toosuccessfully determinar Hola mantenimiento y el estado del clúster de hello mientras se está creando.</span><span class="sxs-lookup"><span data-stu-id="fc559-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="fc559-121">Si cambia cualquier configuración en el clúster que afecta a estos servicios, debe utilizar las funciones de aplicación auxiliar de Hola que se proporcionan.</span><span class="sxs-lookup"><span data-stu-id="fc559-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="fc559-122">Para obtener más información sobre las funciones auxiliares, consulte [Desarrollo de la acción de script con HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="fc559-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="fc559-123">salida de Hello y registros de errores de Hola para script de Hola se almacenan en la cuenta de almacenamiento predeterminada de Hola que especificó para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="fc559-124">Hello registros almacenan en una tabla con nombre de hello **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="fc559-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="fc559-125">Se trata de registros agregados desde un script de Hola ejecutar en todos los nodos de hello (nodo principal y nodos de trabajador) en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="fc559-126">Cada clúster puede aceptar varias acciones de script que se invocan en orden de hello en el que se especifican.</span><span class="sxs-lookup"><span data-stu-id="fc559-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="fc559-127">Una secuencia de comandos se pueda ejecutar en el nodo principal de hello, nodos de trabajador de Hola o ambos.</span><span class="sxs-lookup"><span data-stu-id="fc559-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="fc559-128">HDInsight proporciona varios Hola de tooinstall de secuencias de comandos de los componentes siguientes en clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="fc559-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="fc559-129">Nombre</span><span class="sxs-lookup"><span data-stu-id="fc559-129">Name</span></span> | <span data-ttu-id="fc559-130">Script</span><span class="sxs-lookup"><span data-stu-id="fc559-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="fc559-131">**Instalar Spark**</span><span class="sxs-lookup"><span data-stu-id="fc559-131">**Install Spark**</span></span> |<span data-ttu-id="fc559-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="fc559-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="fc559-133">Vea [Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="fc559-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="fc559-134">**Instalar R**</span><span class="sxs-lookup"><span data-stu-id="fc559-134">**Install R**</span></span> |<span data-ttu-id="fc559-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="fc559-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="fc559-136">Consulte [Instalación y uso de R en clústeres de HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="fc559-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="fc559-137">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="fc559-137">**Install Solr**</span></span> |<span data-ttu-id="fc559-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="fc559-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="fc559-139">Vea [Instalación y uso de Solr en clústeres de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="fc559-140">- **Instalar Giraph**</span><span class="sxs-lookup"><span data-stu-id="fc559-140">- **Install Giraph**</span></span> |<span data-ttu-id="fc559-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="fc559-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="fc559-142">Vea [Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="fc559-143">**Carga previa de las bibliotecas de Hive**</span><span class="sxs-lookup"><span data-stu-id="fc559-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="fc559-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="fc559-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="fc559-145">Vea [Incorporación de bibliotecas de Hive durante la creación de clústeres de HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="fc559-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="fc559-146">Llamar a secuencias de comandos mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="fc559-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="fc559-147">**De hello portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="fc559-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="fc559-148">Comience a crear un clúster, tal y como se describe en [Creación de clústeres de Hadoop en HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="fc559-149">En configuración opcional para hello **acciones de Script** hoja, haga clic en **Agregar acción de secuencia de comandos** tooprovide detalles sobre la acción de secuencia de comandos de hello, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="fc559-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="fc559-150">![Use la acción de secuencia de comandos toocustomize un clúster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize de acción de secuencia de comandos de uso un clúster")</span><span class="sxs-lookup"><span data-stu-id="fc559-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="fc559-151">Propiedad</span><span class="sxs-lookup"><span data-stu-id="fc559-151">Property</span></span></th><th><span data-ttu-id="fc559-152">Valor</span><span class="sxs-lookup"><span data-stu-id="fc559-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="fc559-153">Nombre</span><span class="sxs-lookup"><span data-stu-id="fc559-153">Name</span></span></td>
            <td><span data-ttu-id="fc559-154">Especifique un nombre para la acción de secuencia de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="fc559-155">Identificador URI de script</span><span class="sxs-lookup"><span data-stu-id="fc559-155">Script URI</span></span></td>
            <td><span data-ttu-id="fc559-156">Especifique Hola URI toohello script que es invocado toocustomize Hola clúster.</span><span class="sxs-lookup"><span data-stu-id="fc559-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="fc559-157">s</span><span class="sxs-lookup"><span data-stu-id="fc559-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="fc559-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="fc559-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="fc559-159">Especifique los nodos de hello (**Head** o **trabajo**) en qué personalización Hola se ejecuta el script.</b>.</span><span class="sxs-lookup"><span data-stu-id="fc559-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="fc559-160">parameters</span><span class="sxs-lookup"><span data-stu-id="fc559-160">Parameters</span></span></td>
            <td><span data-ttu-id="fc559-161">Especificar parámetros de hello, si así lo requiere el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="fc559-162">Presione ENTRAR tooadd más de una secuencia de comandos acción tooinstall varios componentes de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="fc559-163">Haga clic en **seleccione** toosave Hola configuración de acción de secuencia de comandos y continuar con la creación del clúster.</span><span class="sxs-lookup"><span data-stu-id="fc559-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="fc559-164">Llamada a scripts con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc559-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="fc559-165">Este script de PowerShell siguiente muestra cómo tooinstall Spark en Windows en la función de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc559-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
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

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
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


<span data-ttu-id="fc559-166">tooinstall otro software, deberá tooreplace archivo de script de Hola en script de Hola:</span><span class="sxs-lookup"><span data-stu-id="fc559-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="fc559-167">Cuando se le solicite, escriba credenciales de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="fc559-168">Puede tardar varios minutos antes de que se crea un clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="fc559-169">Llamada a scripts mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fc559-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="fc559-170">Hello en el ejemplo siguiente se muestra cómo tooinstall Spark en Windows en la función de clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc559-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="fc559-171">tooinstall otro software, deberá tooreplace archivo de script de hello en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="fc559-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="fc559-172">**un clúster de HDInsight con Spark toocreate**</span><span class="sxs-lookup"><span data-stu-id="fc559-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="fc559-173">Cree una aplicación de consola en C# mediante Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fc559-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="fc559-174">Desde la consola de administrador de paquetes de Nuget hello, ejecute hello siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="fc559-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="fc559-175">Hola de uso después de usar las instrucciones en el archivo Program.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="fc559-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="fc559-176">Coloque el código de hello en clase hello con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="fc559-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
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
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="fc559-177">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="fc559-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="fc559-178">Soporte técnico para el software de código abierto utilizado en clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="fc559-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="fc559-179">Hola servicio HDInsight de Azure de Microsoft es una plataforma flexible que permite toobuild aplicaciones de grandes cantidades de datos en la nube de hello mediante el uso de un ecosistema de tecnologías de código abierto formado alrededor de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="fc559-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="fc559-180">Microsoft Azure proporciona un nivel de compatibilidad general para las tecnologías de código abierto, como se describe en hello **admite ámbito** sección de hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">sitio Web de preguntas frecuentes de soporte de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="fc559-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="fc559-181">Hola servicio HDInsight proporciona un nivel adicional de compatibilidad con algunos componentes de hello, tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="fc559-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="fc559-182">Hay dos tipos de componentes de código abierto que están disponibles en hello servicio HDInsight:</span><span class="sxs-lookup"><span data-stu-id="fc559-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="fc559-183">**Componentes integrados** -estos componentes se instalan previamente en clústeres de HDInsight y proporcionan la funcionalidad básica de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="fc559-184">Por ejemplo, ResourceManager hilo, lenguaje de consulta de Hive hello (HiveQL) y biblioteca de Mahout Hola pertenecen toothis categoría.</span><span class="sxs-lookup"><span data-stu-id="fc559-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="fc559-185">Una lista completa de componentes del clúster está disponible en [cuáles son las novedades en las versiones de clúster de Hadoop Hola proporcionadas por HDInsight?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="fc559-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="fc559-186">**Componentes personalizados** -, como un usuario del clúster hello, puede instalar o usar en la carga de trabajo cualquier componente disponible en la Comunidad de Hola o creado por el usuario.</span><span class="sxs-lookup"><span data-stu-id="fc559-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="fc559-187">Componentes integrados son totalmente compatibles, y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="fc559-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="fc559-188">Componentes suministrados con clúster de HDInsight de hello son totalmente compatibles y Microsoft Support le ayudarán tooisolate y resolver los problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="fc559-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="fc559-189">Componentes personalizados reciben soporte comercialmente razonable toohelp toofurther solucionar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="fc559-190">Esto podría producir en resolver el problema de hello ni pedir que tooengage canales disponibles para hello abrir tecnologías de origen donde se encuentra la amplia experiencia para que la tecnología.</span><span class="sxs-lookup"><span data-stu-id="fc559-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="fc559-191">Por ejemplo, hay diversos sitios de la comunidad que se pueden usar, como el [foro de MSDN para HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Además, los proyectos de Apache tienen sitios del proyecto en [http://apache.org](http://apache.org), por ejemplo, [Hadoop](http://hadoop.apache.org/) y [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="fc559-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="fc559-192">Hola servicio HDInsight proporciona varias maneras de componentes personalizados de toouse.</span><span class="sxs-lookup"><span data-stu-id="fc559-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="fc559-193">Independientemente de cómo un componente se utiliza o instalado en el clúster de hello, hello mismo nivel de compatibilidad se aplica.</span><span class="sxs-lookup"><span data-stu-id="fc559-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="fc559-194">A continuación se muestra una lista de las maneras más habituales de Hola que los componentes personalizados pueden utilizarse en clústeres de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="fc559-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="fc559-195">Envío de trabajos - Hadoop u otros tipos de trabajos que se ejecutan o utilizan componentes personalizados pueden clúster toohello enviado.</span><span class="sxs-lookup"><span data-stu-id="fc559-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="fc559-196">Personalización de clúster - durante la creación del clúster, puede especificar opciones de configuración adicionales y componentes personalizados que se instalarán en los nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="fc559-197">Ejemplos: para componentes personalizados populares, Microsoft y otros elementos pueden proporcionar ejemplos de cómo se pueden usar estos componentes en clústeres de HDInsight Hola.</span><span class="sxs-lookup"><span data-stu-id="fc559-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="fc559-198">Estas muestras se proporcionan sin soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="fc559-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="fc559-199">Desarrollo de scripts de acción de script</span><span class="sxs-lookup"><span data-stu-id="fc559-199">Develop Script Action scripts</span></span>
<span data-ttu-id="fc559-200">Consulte [Desarrollo de scripts de acciones de script con HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="fc559-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="fc559-201">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="fc559-201">See also</span></span>
* <span data-ttu-id="fc559-202">[Crear clústeres de Hadoop en HDInsight] [ hdinsight-provision-cluster] proporciona instrucciones sobre cómo toocreate una HDInsight de clúster mediante el uso de otras opciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="fc559-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="fc559-203">[Desarrollo de acciones de script con HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="fc559-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="fc559-204">[Instalación y uso de Spark en clústeres de HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="fc559-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="fc559-205">[Instalación y uso de R en clústeres de Hadoop de HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="fc559-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="fc559-206">[Instalación y uso de Solr en clústeres de Hadoop de HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="fc559-207">[Instalación y uso de Giraph en clústeres de HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="fc559-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Fases durante la creación del clúster"
