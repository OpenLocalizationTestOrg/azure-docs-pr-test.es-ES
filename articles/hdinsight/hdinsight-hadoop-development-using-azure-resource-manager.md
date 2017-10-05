---
title: "Migración a herramientas de Azure Resource Manager para HDInsight | Microsoft Docs"
description: "Migración a las herramientas de desarrollo de Azure Resource Manager para clústeres de HDInsight"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="eace7-103">Migración a las herramientas de desarrollo basadas en Azure Resource Manager para clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="eace7-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="eace7-104">HDInsight está abandonando el uso de herramientas basadas en Azure Service Manager (ASM) para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eace7-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="eace7-105">Si ha estado usando Azure PowerShell, la CLI de Azure o el SDK de .NET de HDInsight para trabajar con clústeres de HDInsight, se le recomienda que utilice las versiones basadas en Azure Resource Manager (ARM) de PowerShell, CLI y del SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="eace7-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="eace7-106">Este artículo proporciona sugerencias sobre cómo migrar al nuevo enfoque basado en ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="eace7-107">Siempre que sea aplicable, este artículo también señala las diferencias entre los enfoques con ASM y con ARM para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eace7-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eace7-108">El soporte para ASM basado en PowerShell, CLI, y SDK de .NET dejará de estar disponible el **1 de enero de 2017**.</span><span class="sxs-lookup"><span data-stu-id="eace7-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="eace7-109">Migración de la CLI de Azure a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eace7-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="eace7-110">La CLI de Azure ahora tiene como valor predeterminado el modo de Azure Resource Manager (ARM), a menos que esté actualizando desde una instalación anterior, en cuyo caso es posible que tenga que utilizar el comando `azure config mode arm` para cambiar al modo ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="eace7-111">Los comandos básicos que la CLI de Azure proporcionaba para trabajar con HDInsight mediante Azure Service Management (ASM) son los mismos que cuando utiliza ARM; sin embargo, algunos parámetros y conmutadores pueden tener nombres nuevos, y hay muchos parámetros nuevos disponibles si utiliza ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="eace7-112">Por ejemplo, ahora puede usar `azure hdinsight cluster create` para especificar la red virtual de Azure en la que se debe crear un clúster o la información de la tienda de metadatos de Hive y Oozie.</span><span class="sxs-lookup"><span data-stu-id="eace7-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="eace7-113">Los comandos básicos para trabajar con HDInsight a través de Azure Resource Manager son:</span><span class="sxs-lookup"><span data-stu-id="eace7-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="eace7-114">`azure hdinsight cluster create` : crea un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="eace7-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="eace7-115">`azure hdinsight cluster delete` : elimina un clúster de HDInsight que ya existe</span><span class="sxs-lookup"><span data-stu-id="eace7-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="eace7-116">`azure hdinsight cluster show` : muestra información acerca de un clúster que ya existe</span><span class="sxs-lookup"><span data-stu-id="eace7-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="eace7-117">`azure hdinsight cluster list` : enumera los clústeres de HDInsight para la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="eace7-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="eace7-118">Utilice el conmutador `-h` para inspeccionar los parámetros y conmutadores disponibles para cada comando.</span><span class="sxs-lookup"><span data-stu-id="eace7-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="eace7-119">Nuevos comandos</span><span class="sxs-lookup"><span data-stu-id="eace7-119">New commands</span></span>
<span data-ttu-id="eace7-120">Los nuevos comandos disponibles con Azure Resource Manager son:</span><span class="sxs-lookup"><span data-stu-id="eace7-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="eace7-121">`azure hdinsight cluster resize` : cambia dinámicamente el número de nodos de trabajo del clúster</span><span class="sxs-lookup"><span data-stu-id="eace7-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="eace7-122">`azure hdinsight cluster enable-http-access` : habilita el acceso HTTP al clúster (de forma predeterminada)</span><span class="sxs-lookup"><span data-stu-id="eace7-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="eace7-123">`azure hdinsight cluster disable-http-access` : deshabilita el acceso HTTP al clúster</span><span class="sxs-lookup"><span data-stu-id="eace7-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="eace7-124">`azure hdinsight script-action`: proporciona comandos para crear y administrar las acciones de script en un clúster</span><span class="sxs-lookup"><span data-stu-id="eace7-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="eace7-125">`azure hdinsight config`: proporciona comandos para crear un archivo de configuración que se puede usar con el comando `hdinsight cluster create` para proporcionar información de configuración.</span><span class="sxs-lookup"><span data-stu-id="eace7-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="eace7-126">Comandos en desuso</span><span class="sxs-lookup"><span data-stu-id="eace7-126">Deprecated commands</span></span>
<span data-ttu-id="eace7-127">Si utiliza los comandos `azure hdinsight job` para enviar trabajos al clúster de HDInsight, estos no estarán disponibles a través de los comandos ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="eace7-128">Si necesita enviar trabajos a HDInsight mediante programación desde scripts, debe usar las API de REST proporcionadas por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eace7-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="eace7-129">Para más información sobre el envío de trabajos mediante las API de REST, consulte los siguientes documentos.</span><span class="sxs-lookup"><span data-stu-id="eace7-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="eace7-130">Ejecución de trabajos de MapReduce con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="eace7-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="eace7-131">Ejecución de consultas de Hive con Hadoop en HDInsight con cURL</span><span class="sxs-lookup"><span data-stu-id="eace7-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="eace7-132">Ejecución de trabajos de Pig con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="eace7-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="eace7-133">Para más información sobre otras formas de ejecutar MapReduce, Hive y Pig interactivamente, consulte [Uso de MapReduce con Hadoop en HDInsight](hdinsight-use-mapreduce.md), [Uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md) y [Uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="eace7-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="eace7-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="eace7-134">Examples</span></span>
<span data-ttu-id="eace7-135">**Creación de un clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-135">**Creating a cluster**</span></span>

* <span data-ttu-id="eace7-136">Comando anterior (ASM): `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="eace7-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="eace7-137">Nuevo comando (ARM): `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="eace7-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="eace7-138">**Eliminación de un cluster**</span><span class="sxs-lookup"><span data-stu-id="eace7-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="eace7-139">Comando anterior (ASM): `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="eace7-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="eace7-140">Nuevo comando (ARM): `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="eace7-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="eace7-141">**Enumeración de clústeres**</span><span class="sxs-lookup"><span data-stu-id="eace7-141">**List clusters**</span></span>

* <span data-ttu-id="eace7-142">Comando anterior (ASM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="eace7-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="eace7-143">Nuevo comando (ARM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="eace7-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="eace7-144">Para el comando list, si especifica el grupo de recursos mediante `-g` devolverá solo los clústeres del grupo de recursos especificado.</span><span class="sxs-lookup"><span data-stu-id="eace7-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="eace7-145">**Presentación de la información de clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-145">**Show cluster information**</span></span>

* <span data-ttu-id="eace7-146">Comando anterior (ASM): `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="eace7-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="eace7-147">Nuevo comando (ARM): `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="eace7-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="eace7-148">Migración de Azure PowerShell a Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eace7-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="eace7-149">La información general acerca de Azure PowerShell en el modo de Azure Resource Manager (ARM) se puede encontrar en [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="eace7-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="eace7-150">Los cmdlets de ARM de Azure PowerShell se pueden instalar en paralelo con los cmdlets de ASM.</span><span class="sxs-lookup"><span data-stu-id="eace7-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="eace7-151">Los cmdlets de los dos modos se pueden distinguir por sus nombres.</span><span class="sxs-lookup"><span data-stu-id="eace7-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="eace7-152">El modo ARM tiene *AzureRmHDInsight* en los nombres de cmdlet en lugar de *AzureHDInsight*, que es lo que aparece en el modo ASM.</span><span class="sxs-lookup"><span data-stu-id="eace7-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="eace7-153">Por ejemplo, *AzureRmHDInsightCluster New* frente a *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="eace7-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="eace7-154">Parámetros y conmutadores pueden tener nombres nuevos y hay muchos parámetros nuevos disponibles si utiliza ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="eace7-155">Por ejemplo, varios cmdlets requieren un nuevo modificador llamado *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="eace7-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="eace7-156">Para poder usar los cmdlets de HDInsight, debe conectarse a su cuenta de Azure y crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="eace7-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="eace7-157">Login-AzureRmAccount o [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="eace7-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="eace7-158">Consulte [Autenticación de una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="eace7-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="eace7-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="eace7-160">Cmdlets cuyo nombre ha cambiado</span><span class="sxs-lookup"><span data-stu-id="eace7-160">Renamed cmdlets</span></span>
<span data-ttu-id="eace7-161">Para enumerar los cmdlets de ASM para HDInsight en la consola de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="eace7-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="eace7-162">En la tabla siguiente se enumeran los cmdlets de ASM y sus nombres en el modo ARM:</span><span class="sxs-lookup"><span data-stu-id="eace7-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="eace7-163">Cmdlets de ASM</span><span class="sxs-lookup"><span data-stu-id="eace7-163">ASM cmdlets</span></span> | <span data-ttu-id="eace7-164">Cmdlets de ARM</span><span class="sxs-lookup"><span data-stu-id="eace7-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="eace7-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="eace7-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="eace7-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="eace7-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="eace7-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="eace7-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="eace7-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="eace7-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="eace7-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="eace7-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="eace7-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="eace7-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="eace7-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="eace7-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="eace7-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="eace7-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="eace7-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="eace7-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="eace7-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="eace7-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="eace7-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="eace7-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="eace7-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="eace7-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="eace7-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="eace7-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="eace7-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="eace7-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="eace7-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="eace7-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="eace7-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="eace7-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="eace7-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="eace7-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="eace7-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="eace7-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="eace7-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="eace7-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="eace7-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="eace7-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="eace7-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="eace7-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="eace7-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="eace7-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="eace7-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="eace7-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="eace7-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="eace7-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="eace7-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="eace7-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="eace7-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="eace7-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="eace7-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="eace7-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="eace7-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="eace7-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="eace7-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="eace7-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="eace7-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="eace7-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="eace7-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="eace7-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="eace7-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="eace7-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="eace7-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="eace7-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="eace7-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="eace7-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="eace7-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="eace7-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="eace7-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="eace7-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="eace7-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="eace7-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="eace7-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="eace7-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="eace7-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="eace7-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="eace7-219">Nuevos cmdlets</span><span class="sxs-lookup"><span data-stu-id="eace7-219">New cmdlets</span></span>
<span data-ttu-id="eace7-220">Los siguientes son los nuevos cmdlets que solo están disponibles en el modo de ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="eace7-221">**Cmdlets relacionados con acciones de script:**</span><span class="sxs-lookup"><span data-stu-id="eace7-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="eace7-222">**Get-AzureRmHDInsightPersistedScriptAction**: obtiene las acciones de script persistentes para un clúster y las muestra en orden cronológico u obtiene detalles de una acción de script persistente concreta.</span><span class="sxs-lookup"><span data-stu-id="eace7-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="eace7-223">**Get-AzureRmHDInsightScriptActionHistory**: obtiene el historial de una acción de script para un clúster y los datos se enumeran en orden cronológico inverso u obtiene detalles de una acción de script ejecutada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="eace7-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="eace7-224">**Remove-AzureRmHDInsightPersistedScriptAction**: quita una acción de script persistente de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eace7-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="eace7-225">**Set-AzureRmHDInsightPersistedScriptAction**: establece una acción de script ejecutada anteriormente para que sea una acción de script persistente.</span><span class="sxs-lookup"><span data-stu-id="eace7-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="eace7-226">**Submit-AzureRmHDInsightScriptAction**: envía una nueva acción de script a un clúster de HDInsight de Azure.</span><span class="sxs-lookup"><span data-stu-id="eace7-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="eace7-227">Para más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="eace7-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="eace7-228">**Cmdlets relacionados con la identidad del clúster:**</span><span class="sxs-lookup"><span data-stu-id="eace7-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="eace7-229">**Add-AzureRmHDInsightClusterIdentity**: agrega una identidad de clúster a un objeto de configuración de clúster para que el clúster de HDInsight pueda acceder a almacenes de Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="eace7-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="eace7-230">Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eace7-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="eace7-231">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="eace7-231">Examples</span></span>
<span data-ttu-id="eace7-232">**Crear clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-232">**Create cluster**</span></span>

<span data-ttu-id="eace7-233">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="eace7-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="eace7-234">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="eace7-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="eace7-235">**Eliminación de clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-235">**Delete cluster**</span></span>

<span data-ttu-id="eace7-236">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="eace7-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="eace7-237">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="eace7-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="eace7-238">**Enumeración de clústeres**</span><span class="sxs-lookup"><span data-stu-id="eace7-238">**List cluster**</span></span>

<span data-ttu-id="eace7-239">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="eace7-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="eace7-240">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="eace7-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="eace7-241">**Presentación de clústeres**</span><span class="sxs-lookup"><span data-stu-id="eace7-241">**Show cluster**</span></span>

<span data-ttu-id="eace7-242">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="eace7-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="eace7-243">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="eace7-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="eace7-244">Otros ejemplos</span><span class="sxs-lookup"><span data-stu-id="eace7-244">Other samples</span></span>
* [<span data-ttu-id="eace7-245">Creación de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="eace7-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="eace7-246">Envío de trabajos de Hive</span><span class="sxs-lookup"><span data-stu-id="eace7-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="eace7-247">Envío de trabajos de Pig</span><span class="sxs-lookup"><span data-stu-id="eace7-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="eace7-248">Envío de trabajos de Sqoop</span><span class="sxs-lookup"><span data-stu-id="eace7-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="eace7-249">Migración al SDK de .NET de HDInsight basado en ARM</span><span class="sxs-lookup"><span data-stu-id="eace7-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="eace7-250">El [SDK de .NET de HDInsight](https://msdn.microsoft.com/library/azure/mt416619.aspx) basado en Azure Service Management (ASM) ya está en desuso.</span><span class="sxs-lookup"><span data-stu-id="eace7-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="eace7-251">Se recomienda utilizar el [SDK de .NET de HDInsight](https://msdn.microsoft.com/library/azure/mt271028.aspx)basado en Azure Resource Management (ARM).</span><span class="sxs-lookup"><span data-stu-id="eace7-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="eace7-252">Los siguientes paquetes de HDInsight basado en ASM quedarán obsoletos.</span><span class="sxs-lookup"><span data-stu-id="eace7-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="eace7-253">Esta sección proporciona indicadores a más información sobre cómo realizar determinadas tareas mediante el SDK de ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="eace7-254">Como... mediante el uso del SDK de .NET de HDInsight basado en ARM</span><span class="sxs-lookup"><span data-stu-id="eace7-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="eace7-255">Vínculos</span><span class="sxs-lookup"><span data-stu-id="eace7-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="eace7-256">Crear clústeres basados en Linux en HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-257">Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="eace7-258">Personalizar un clúster mediante una acción de script con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="eace7-259">Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="eace7-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="eace7-260">Autenticar interactivamente aplicaciones mediante Azure Active Directory con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="eace7-261">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="eace7-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="eace7-262">El fragmento de código de este artículo usa el enfoque de autenticación interactiva.</span><span class="sxs-lookup"><span data-stu-id="eace7-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="eace7-263">Autenticar aplicaciones de forma no interactiva mediante Azure Active Directory con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="eace7-264">Consulte [Crear aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="eace7-265">Enviar un trabajo de Hive mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="eace7-266">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="eace7-267">Enviar un trabajo de Pig mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="eace7-268">Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="eace7-269">Enviar un trabajo de Sqoop mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="eace7-270">Consulte [Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="eace7-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="eace7-271">Enumerar clústeres de HDInsight con el SDK. de .NET.</span><span class="sxs-lookup"><span data-stu-id="eace7-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-272">Consulte [Enumeración de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="eace7-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="eace7-273">Escalar clústeres de HDInsight con el SDK. de .NET.</span><span class="sxs-lookup"><span data-stu-id="eace7-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-274">Consulte [Escalamiento de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="eace7-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="eace7-275">Conceder o revocar acceso a los clústeres de HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-276">Consulte [Concesión o revocamiento de acceso a los clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="eace7-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="eace7-277">Actualizar las credenciales de usuario HTTP para clústeres de HDInsight mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-278">Consulte [Actualización de las credenciales de usuario HTTP para clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="eace7-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="eace7-279">Encontrar la cuenta de almacenamiento predeterminada para los clústeres de HDInsight mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="eace7-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-280">Consulte [Búsqueda de la cuenta de almacenamiento predeterminada para los clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="eace7-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="eace7-281">Eliminar clústeres de HDInsight con el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="eace7-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="eace7-282">Consulte [Eliminación de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="eace7-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="eace7-283">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="eace7-283">Examples</span></span>
<span data-ttu-id="eace7-284">A continuación se muestran algunos ejemplos de cómo se realiza una operación mediante el SDK basado en ASM y el fragmento de código equivalente para el SDK basado en ARM.</span><span class="sxs-lookup"><span data-stu-id="eace7-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="eace7-285">**Creación de un cliente CRUD de clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="eace7-286">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="eace7-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="eace7-287">Nuevo comando (ARM) (autorización de la entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="eace7-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="eace7-288">Nuevo comando (ARM) (autorización de usuario)</span><span class="sxs-lookup"><span data-stu-id="eace7-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="eace7-289">**Creación de un clúster**</span><span class="sxs-lookup"><span data-stu-id="eace7-289">**Creating a cluster**</span></span>

* <span data-ttu-id="eace7-290">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="eace7-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="eace7-291">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="eace7-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="eace7-292">**Habilitación del acceso HTTP**</span><span class="sxs-lookup"><span data-stu-id="eace7-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="eace7-293">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="eace7-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="eace7-294">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="eace7-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="eace7-295">**Eliminación de un cluster**</span><span class="sxs-lookup"><span data-stu-id="eace7-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="eace7-296">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="eace7-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="eace7-297">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="eace7-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

