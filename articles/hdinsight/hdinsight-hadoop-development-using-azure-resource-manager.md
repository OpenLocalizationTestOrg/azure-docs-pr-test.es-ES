---
title: aaaMigrate tooAzure el Administrador de recursos de las herramientas de HDInsight | Documentos de Microsoft
description: "Cómo las herramientas toomigrate tooAzure desarrollo del Administrador de recursos para clústeres de HDInsight"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="bbd53-103">Herramientas de desarrollo basado en el Administrador de recursos tooAzure migrar para clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd53-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="bbd53-104">HDInsight está abandonando el uso de herramientas basadas en Azure Service Manager (ASM) para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbd53-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="bbd53-105">Si se ha usando Azure PowerShell, CLI de Azure o hello HDInsight .NET SDK toowork con clústeres de HDInsight, son toouse recomienda Hola basado en ARM de administrador de recursos de Azure versiones de PowerShell, CLI y .NET SDK en el futuro.</span><span class="sxs-lookup"><span data-stu-id="bbd53-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="bbd53-106">Este artículo proporciona punteros acerca de cómo toomigrate toohello nuevo basado en ARM enfoque.</span><span class="sxs-lookup"><span data-stu-id="bbd53-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="bbd53-107">Siempre que sea aplicable, este artículo también señala las diferencias de hello entre los enfoques ASM y ARM de Hola para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbd53-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbd53-108">soporte de Hola para ASM basada en PowerShell, CLI, y dejará de SDK de .NET en **del 1 de enero de 2017**.</span><span class="sxs-lookup"><span data-stu-id="bbd53-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="bbd53-109">Migrar tooAzure de CLI de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bbd53-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="bbd53-110">Hola CLI de Azure ahora tiene como valor predeterminado el modo de tooAzure Resource Manager (ARM), a menos que se va a actualizar desde una instalación anterior; en este caso, deberá toouse hello `azure config mode arm` modo de comando tooswitch tooARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="bbd53-111">comandos básicos de Hola que Hola CLI de Azure proporciona toowork con HDInsight con la administración de servicio de Azure (ASM) se Hola igual al usar ARM; Sin embargo algunos parámetros y modificadores de pueden tener nombres nuevos, y hay muchos nuevos parámetros disponibles cuando se usa ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="bbd53-112">Por ejemplo, ahora puede usar `azure hdinsight cluster create` toospecify Hola red Virtual de Azure que deben crearse en un clúster, o subárbol e información de la tienda de metadatos de Oozie.</span><span class="sxs-lookup"><span data-stu-id="bbd53-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="bbd53-113">Los comandos básicos para trabajar con HDInsight a través de Azure Resource Manager son:</span><span class="sxs-lookup"><span data-stu-id="bbd53-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="bbd53-114">`azure hdinsight cluster create` : crea un clúster de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd53-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="bbd53-115">`azure hdinsight cluster delete` : elimina un clúster de HDInsight que ya existe</span><span class="sxs-lookup"><span data-stu-id="bbd53-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="bbd53-116">`azure hdinsight cluster show` : muestra información acerca de un clúster que ya existe</span><span class="sxs-lookup"><span data-stu-id="bbd53-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="bbd53-117">`azure hdinsight cluster list` : enumera los clústeres de HDInsight para la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="bbd53-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="bbd53-118">Hola de uso `-h` cambiar los parámetros de hello tooinspect y modificadores disponibles para cada comando.</span><span class="sxs-lookup"><span data-stu-id="bbd53-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="bbd53-119">Nuevos comandos</span><span class="sxs-lookup"><span data-stu-id="bbd53-119">New commands</span></span>
<span data-ttu-id="bbd53-120">Los nuevos comandos disponibles con Azure Resource Manager son:</span><span class="sxs-lookup"><span data-stu-id="bbd53-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="bbd53-121">`azure hdinsight cluster resize`-dinámicamente cambios Hola número de nodos de trabajador del clúster Hola</span><span class="sxs-lookup"><span data-stu-id="bbd53-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="bbd53-122">`azure hdinsight cluster enable-http-access`-permite HTTPs acceso toohello clúster (de forma predeterminada)</span><span class="sxs-lookup"><span data-stu-id="bbd53-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="bbd53-123">`azure hdinsight cluster disable-http-access`-deshabilita el clúster de toohello de acceso de HTTPs</span><span class="sxs-lookup"><span data-stu-id="bbd53-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="bbd53-124">`azure hdinsight script-action` : proporciona comandos para crear y administrar las acciones de script en un clúster</span><span class="sxs-lookup"><span data-stu-id="bbd53-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="bbd53-125">`azure hdinsight config`-proporciona comandos para crear un archivo de configuración que se puede usar con hello `hdinsight cluster create` comando tooprovide la información de configuración.</span><span class="sxs-lookup"><span data-stu-id="bbd53-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="bbd53-126">Comandos en desuso</span><span class="sxs-lookup"><span data-stu-id="bbd53-126">Deprecated commands</span></span>
<span data-ttu-id="bbd53-127">Si usas hello `azure hdinsight job` clúster de HDInsight de comandos toosubmit trabajos tooyour, estos no están disponibles a través de los comandos de hello ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="bbd53-128">Si necesita tooprogrammatically enviar trabajos tooHDInsight desde secuencias de comandos, debe usar en su lugar hello las API de REST proporcionada por HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbd53-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="bbd53-129">Para obtener más información sobre cómo enviar trabajos mediante las API de REST, vea Hola después de documentos.</span><span class="sxs-lookup"><span data-stu-id="bbd53-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="bbd53-130">Ejecución de trabajos de MapReduce con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="bbd53-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="bbd53-131">Ejecución de consultas de Hive con Hadoop en HDInsight con cURL</span><span class="sxs-lookup"><span data-stu-id="bbd53-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="bbd53-132">Ejecución de trabajos de Pig con Hadoop en HDInsight con Curl</span><span class="sxs-lookup"><span data-stu-id="bbd53-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="bbd53-133">Para obtener información sobre otro toorun formas MapReduce, Hive, Pig de forma interactiva, consulte [MapReduce de uso con Hadoop en HDInsight](hdinsight-use-mapreduce.md), [uso de Hive con Hadoop en HDInsight](hdinsight-use-hive.md), y [uso de Pig con Hadoop en HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="bbd53-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="bbd53-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbd53-134">Examples</span></span>
<span data-ttu-id="bbd53-135">**Creación de un clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-135">**Creating a cluster**</span></span>

* <span data-ttu-id="bbd53-136">Comando anterior (ASM): `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="bbd53-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="bbd53-137">Nuevo comando (ARM): `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="bbd53-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="bbd53-138">**Eliminación de un cluster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="bbd53-139">Comando anterior (ASM): `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="bbd53-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="bbd53-140">Nuevo comando (ARM): `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="bbd53-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="bbd53-141">**Enumeración de clústeres**</span><span class="sxs-lookup"><span data-stu-id="bbd53-141">**List clusters**</span></span>

* <span data-ttu-id="bbd53-142">Comando anterior (ASM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="bbd53-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="bbd53-143">Nuevo comando (ARM): `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="bbd53-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="bbd53-144">Comando de lista de hello, especificar Hola grupo de recursos mediante `-g` devolverá solo los clústeres de hello en el grupo de recursos especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="bbd53-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="bbd53-145">**Presentación de la información de clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-145">**Show cluster information**</span></span>

* <span data-ttu-id="bbd53-146">Comando anterior (ASM): `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="bbd53-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="bbd53-147">Nuevo comando (ARM): `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="bbd53-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="bbd53-148">Migrar tooAzure de PowerShell de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bbd53-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="bbd53-149">Hola obtener información general acerca de PowerShell de Azure en el modo de hello Azure Resource Manager (ARM) puede encontrarse en [con Azure PowerShell con el Administrador de recursos de Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bbd53-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="bbd53-150">Hola cmdlets de ARM de PowerShell de Azure puede ser instalado en paralelo con hello ASM cmdlets.</span><span class="sxs-lookup"><span data-stu-id="bbd53-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="bbd53-151">cmdlets de Hola de dos modos de Hola se pueden distinguir por sus nombres.</span><span class="sxs-lookup"><span data-stu-id="bbd53-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="bbd53-152">el modo de Hello ARM tiene *AzureRmHDInsight* en nombres de cmdlet de hello comparar demasiado*AzureHDInsight* en modo ASM de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbd53-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="bbd53-153">Por ejemplo, *AzureRmHDInsightCluster New* frente a *New-AzureHDInsightCluster*.</span><span class="sxs-lookup"><span data-stu-id="bbd53-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="bbd53-154">Parámetros y conmutadores pueden tener nombres nuevos y hay muchos parámetros nuevos disponibles si utiliza ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="bbd53-155">Por ejemplo, varios cmdlets requieren un nuevo modificador llamado *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="bbd53-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="bbd53-156">Antes de poder usar cmdlets de HDInsight de hello, debe conectarse tooyour cuenta de Azure y crear un nuevo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="bbd53-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="bbd53-157">Login-AzureRmAccount o [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbd53-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="bbd53-158">Consulte [Autenticación de una entidad de servicio con el Administrador de recursos de Azure](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="bbd53-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bbd53-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="bbd53-160">Cmdlets cuyo nombre ha cambiado</span><span class="sxs-lookup"><span data-stu-id="bbd53-160">Renamed cmdlets</span></span>
<span data-ttu-id="bbd53-161">Hola toolist cmdlets de HDInsight ASM en la consola de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bbd53-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="bbd53-162">Hello tabla siguiente enumeran Hola ASM cmdlets y sus nombres en el modo de hello ARM:</span><span class="sxs-lookup"><span data-stu-id="bbd53-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="bbd53-163">Cmdlets de ASM</span><span class="sxs-lookup"><span data-stu-id="bbd53-163">ASM cmdlets</span></span> | <span data-ttu-id="bbd53-164">Cmdlets de ARM</span><span class="sxs-lookup"><span data-stu-id="bbd53-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="bbd53-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="bbd53-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="bbd53-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="bbd53-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="bbd53-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="bbd53-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="bbd53-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="bbd53-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="bbd53-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="bbd53-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="bbd53-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="bbd53-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="bbd53-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="bbd53-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="bbd53-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="bbd53-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="bbd53-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="bbd53-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="bbd53-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="bbd53-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="bbd53-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="bbd53-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="bbd53-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="bbd53-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="bbd53-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="bbd53-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="bbd53-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="bbd53-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="bbd53-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="bbd53-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="bbd53-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="bbd53-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="bbd53-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="bbd53-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="bbd53-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="bbd53-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="bbd53-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="bbd53-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="bbd53-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="bbd53-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="bbd53-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="bbd53-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="bbd53-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="bbd53-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="bbd53-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="bbd53-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="bbd53-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="bbd53-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="bbd53-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="bbd53-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="bbd53-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="bbd53-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="bbd53-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="bbd53-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="bbd53-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="bbd53-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="bbd53-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="bbd53-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="bbd53-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="bbd53-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="bbd53-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="bbd53-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="bbd53-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="bbd53-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="bbd53-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="bbd53-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="bbd53-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="bbd53-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="bbd53-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="bbd53-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="bbd53-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="bbd53-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="bbd53-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="bbd53-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="bbd53-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="bbd53-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="bbd53-219">Nuevos cmdlets</span><span class="sxs-lookup"><span data-stu-id="bbd53-219">New cmdlets</span></span>
<span data-ttu-id="bbd53-220">los siguientes Hola son Hola nuevos cmdlets que solo están disponibles en el modo de hello ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="bbd53-221">**Cmdlets relacionados con acciones de script:**</span><span class="sxs-lookup"><span data-stu-id="bbd53-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="bbd53-222">**Get-AzureRmHDInsightPersistedScriptAction**: Hola obtiene conserva las acciones de script para un clúster y muestra los resultados en orden cronológico u obtiene detalles de una acción de script persistentes especificado.</span><span class="sxs-lookup"><span data-stu-id="bbd53-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="bbd53-223">**Get-AzureRmHDInsightScriptActionHistory**: Obtiene el historial de acciones de script de Hola para un clúster y se enumeran en orden cronológico inverso u obtiene detalles de una acción de secuencia de comandos ejecutada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bbd53-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="bbd53-224">**Remove-AzureRmHDInsightPersistedScriptAction**: quita una acción de script persistente de un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bbd53-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="bbd53-225">**Conjunto AzureRmHDInsightPersistedScriptAction**: establece un toobe de acción de secuencia de comandos ejecutada con anterioridad una acción de script persistentes.</span><span class="sxs-lookup"><span data-stu-id="bbd53-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="bbd53-226">**AzureRmHDInsightScriptAction enviar**: envía un nuevo clúster de HDInsight de Azure de tooan de acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="bbd53-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="bbd53-227">Para más información, consulte [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bbd53-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="bbd53-228">**Cmdlets relacionados con la identidad del clúster:**</span><span class="sxs-lookup"><span data-stu-id="bbd53-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="bbd53-229">**AzureRmHDInsightClusterIdentity agregar**: agrega un objeto de configuración de clúster de clúster identidad tooa de modo que hello clúster de HDInsight puede tener acceso a almacenes de datos Lake de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbd53-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="bbd53-230">Consulte [Creación de un clúster de HDInsight con el Almacén de Data Lake mediante Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bbd53-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="bbd53-231">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbd53-231">Examples</span></span>
<span data-ttu-id="bbd53-232">**Crear clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-232">**Create cluster**</span></span>

<span data-ttu-id="bbd53-233">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="bbd53-234">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-234">New command (ARM):</span></span>

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


<span data-ttu-id="bbd53-235">**Eliminación de clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-235">**Delete cluster**</span></span>

<span data-ttu-id="bbd53-236">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="bbd53-237">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="bbd53-238">**Enumeración de clústeres**</span><span class="sxs-lookup"><span data-stu-id="bbd53-238">**List cluster**</span></span>

<span data-ttu-id="bbd53-239">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="bbd53-240">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="bbd53-241">**Presentación de clústeres**</span><span class="sxs-lookup"><span data-stu-id="bbd53-241">**Show cluster**</span></span>

<span data-ttu-id="bbd53-242">Comando anterior (ASM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="bbd53-243">Nuevo comando (ARM):</span><span class="sxs-lookup"><span data-stu-id="bbd53-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="bbd53-244">Otros ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbd53-244">Other samples</span></span>
* [<span data-ttu-id="bbd53-245">Creación de clústeres de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd53-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="bbd53-246">Envío de trabajos de Hive</span><span class="sxs-lookup"><span data-stu-id="bbd53-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="bbd53-247">Envío de trabajos de Pig</span><span class="sxs-lookup"><span data-stu-id="bbd53-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="bbd53-248">Envío de trabajos de Sqoop</span><span class="sxs-lookup"><span data-stu-id="bbd53-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="bbd53-249">Migrar toohello basado en ARM HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="bbd53-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="bbd53-250">Hola basado en administración de servicios de Azure [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) ahora está en desuso.</span><span class="sxs-lookup"><span data-stu-id="bbd53-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="bbd53-251">Son toouse recomienda Hola basado en administración de recursos de Azure [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbd53-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="bbd53-252">Hello siguientes paquetes de HDInsight basados en ASM están en desuso.</span><span class="sxs-lookup"><span data-stu-id="bbd53-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="bbd53-253">Esta sección proporciona punteros toomore información acerca de cómo tooperform determinada tareas mediante Hola SDK basado en ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="bbd53-254">Cómo... utilizando Hola basado en ARM SDK de HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd53-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="bbd53-255">Vínculos</span><span class="sxs-lookup"><span data-stu-id="bbd53-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="bbd53-256">Crear clústeres basados en Linux en HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-257">Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="bbd53-258">Personalizar un clúster mediante una acción de script con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="bbd53-259">Consulte [Crear clústeres basados en Linux en HDInsight con el SDK de .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="bbd53-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="bbd53-260">Autenticar interactivamente aplicaciones mediante Azure Active Directory con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="bbd53-261">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="bbd53-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="bbd53-262">fragmento de código de Hello en este artículo utiliza el método de autenticación interactiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbd53-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="bbd53-263">Autenticar aplicaciones de forma no interactiva mediante Azure Active Directory con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="bbd53-264">Consulte [Crear aplicaciones .NET para HDInsight de autenticación no interactiva](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="bbd53-265">Enviar un trabajo de Hive mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="bbd53-266">Consulte [Ejecución de consultas de Hive mediante el SDK de .NET de HDInsight](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="bbd53-267">Enviar un trabajo de Pig mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="bbd53-268">Consulte [Ejecución de trabajos de Pig con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="bbd53-269">Enviar un trabajo de Sqoop mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="bbd53-270">Consulte [Ejecución de trabajos de Sqoop con el SDK de .NET para Hadoop en HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="bbd53-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="bbd53-271">Enumerar clústeres de HDInsight con el SDK. de .NET.</span><span class="sxs-lookup"><span data-stu-id="bbd53-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-272">Consulte [Enumeración de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="bbd53-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="bbd53-273">Escalar clústeres de HDInsight con el SDK. de .NET.</span><span class="sxs-lookup"><span data-stu-id="bbd53-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-274">Consulte [Escalamiento de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="bbd53-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="bbd53-275">Conceder o revocar acceso tooHDInsight clústeres con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-276">Vea [tooHDInsight clústeres de conceder o revocar acceso](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="bbd53-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="bbd53-277">Actualizar las credenciales de usuario HTTP para clústeres de HDInsight mediante el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-278">Consulte [Actualización de las credenciales de usuario HTTP para clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="bbd53-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="bbd53-279">Buscar la cuenta de almacenamiento predeterminada de Hola para clústeres de HDInsight con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="bbd53-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-280">Vea [encontrar la cuenta de almacenamiento predeterminada de Hola para clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="bbd53-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="bbd53-281">Eliminar clústeres de HDInsight con el SDK de .NET.</span><span class="sxs-lookup"><span data-stu-id="bbd53-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="bbd53-282">Consulte [Eliminación de clústeres de HDInsight](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="bbd53-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="bbd53-283">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbd53-283">Examples</span></span>
<span data-ttu-id="bbd53-284">Estos son algunos ejemplos de cómo es una operación efectúa a través de fragmento de código equivalentes de Hola y de saludo SDK de ASM de hello SDK basado en ARM.</span><span class="sxs-lookup"><span data-stu-id="bbd53-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="bbd53-285">**Creación de un cliente CRUD de clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="bbd53-286">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="bbd53-287">Nuevo comando (ARM) (autorización de la entidad de servicio)</span><span class="sxs-lookup"><span data-stu-id="bbd53-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="bbd53-288">Nuevo comando (ARM) (autorización de usuario)</span><span class="sxs-lookup"><span data-stu-id="bbd53-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="bbd53-289">**Creación de un clúster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-289">**Creating a cluster**</span></span>

* <span data-ttu-id="bbd53-290">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="bbd53-291">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="bbd53-292">**Habilitación del acceso HTTP**</span><span class="sxs-lookup"><span data-stu-id="bbd53-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="bbd53-293">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="bbd53-294">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="bbd53-295">**Eliminación de un cluster**</span><span class="sxs-lookup"><span data-stu-id="bbd53-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="bbd53-296">Comando anterior (ASM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="bbd53-297">Nuevo comando (ARM)</span><span class="sxs-lookup"><span data-stu-id="bbd53-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

