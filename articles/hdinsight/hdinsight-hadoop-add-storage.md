---
title: "Adición de cuentas de almacenamiento de Azure a HDInsight | Microsoft Docs"
description: "Aprenda a agregar cuentas de Azure Storage adicionales a un clúster de HDInsight existente."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="97638-103">Adición de más cuentas de almacenamiento a HDInsight</span><span class="sxs-lookup"><span data-stu-id="97638-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="97638-104">Aprenda a usar acciones de script para agregar cuentas de almacenamiento de Azure adicionales a HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="97638-105">Los pasos descritos en este documento agregan una cuenta de almacenamiento a un clúster de HDInsight existente basado en Linux.</span><span class="sxs-lookup"><span data-stu-id="97638-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97638-106">La información de este documento trata sobre cómo agregar almacenamiento adicional a un clúster después de que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="97638-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="97638-107">Para más información sobre cómo agregar cuentas de almacenamiento durante la creación del clúster, consulte [Configuración de clústeres de HDInsight con Hadoop, Spark, Kafka y mucho más](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="97638-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="97638-108">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="97638-108">How it works</span></span>

<span data-ttu-id="97638-109">Este script toma los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="97638-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="97638-110">__Nombre de la cuenta de almacenamiento de Azure__: el nombre de la cuenta de almacenamiento que se agregará al clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="97638-111">Después de ejecutar el script, HDInsight podrá leer y escribir los datos almacenados en esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="97638-112">__Clave de la cuenta de almacenamiento de Azure__: una clave que concede acceso a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="97638-113">__-p__ (opcional): si se especifica, la clave no se cifra y se almacena en el archivo core-site.xml como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="97638-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="97638-114">Durante el procesamiento, el script realiza las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="97638-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="97638-115">Si la cuenta de almacenamiento ya existe en la configuración de core-site.xml para el clúster, el script se cierra y no se lleva a cabo ninguna otra acción.</span><span class="sxs-lookup"><span data-stu-id="97638-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="97638-116">Comprueba que la cuenta de almacenamiento existe y que se puede acceder a ella mediante la clave.</span><span class="sxs-lookup"><span data-stu-id="97638-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="97638-117">Cifra la clave con la credencial del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="97638-118">Agrega la cuenta de almacenamiento al archivo core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="97638-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="97638-119">Detiene y reinicia los servicios de Oozie, YARN, MapReduce2 y HDFS.</span><span class="sxs-lookup"><span data-stu-id="97638-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="97638-120">Detener e iniciar estos servicios permite que usen la nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="97638-121">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="97638-122">La secuencia de comandos</span><span class="sxs-lookup"><span data-stu-id="97638-122">The script</span></span>

<span data-ttu-id="97638-123">__Ubicación del script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="97638-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="97638-124">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="97638-124">__Requirements__:</span></span>

* <span data-ttu-id="97638-125">El script se debe aplicar en los __nodos principales__.</span><span class="sxs-lookup"><span data-stu-id="97638-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="97638-126">Para usar el script</span><span class="sxs-lookup"><span data-stu-id="97638-126">To use the script</span></span>

<span data-ttu-id="97638-127">Este script se puede utilizar a través de Azure Portal, Azure PowerShell o la CLI de Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="97638-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="97638-128">Para más información, consulte el documento [Personalización de clústeres de HDInsight mediante la acción de scripts (Linux)](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="97638-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97638-129">Al utilizar los pasos indicados en el documento de personalización, utilice la siguiente información para aplicar este script:</span><span class="sxs-lookup"><span data-stu-id="97638-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="97638-130">Sustituya el identificador URI de la acción de script necesaria por el identificador URI de este script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="97638-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="97638-131">Reemplace los parámetros de ejemplo por el nombre de la cuenta de almacenamiento de Azure y la clave de la cuenta de almacenamiento que va a agregar al clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="97638-132">Si usa Azure Portal, estos parámetros deben estar separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="97638-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="97638-133">No es necesario marcar este script como __Guardado__, porque actualiza directamente la configuración de Ambari para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="97638-134">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="97638-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="97638-135">Cuentas de almacenamiento que no se muestran en Azure Portal o las herramientas</span><span class="sxs-lookup"><span data-stu-id="97638-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="97638-136">Cuando vea el clúster de HDInsight en Azure Portal, si selecciona la entrada __Cuentas de almacenamiento__ en __Propiedades__, no se mostrarán las cuentas de almacenamiento agregadas mediante esta acción de script.</span><span class="sxs-lookup"><span data-stu-id="97638-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="97638-137">Azure PowerShell y la CLI de Azure tampoco mostrarán la cuenta de almacenamiento adicional.</span><span class="sxs-lookup"><span data-stu-id="97638-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="97638-138">Esto se debe a que el script solo modifica la configuración de core-site.xml del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="97638-139">Esta información no se usa al recuperar la información del clúster mediante las API de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="97638-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="97638-140">Para ver información de la cuenta de almacenamiento agregada al clúster mediante este script, use la API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="97638-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="97638-141">Use los siguientes comandos para recuperar esta información para su clúster:</span><span class="sxs-lookup"><span data-stu-id="97638-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="97638-142">Establezca `$clusterName` en el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="97638-143">Establezca `$storageAccountName` en el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="97638-144">Cuando se le solicite, escriba el nombre de usuario y la contraseña de administrador del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="97638-145">Establezca `$PASSWORD` en la contraseña de cuenta de inicio de sesión del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="97638-146">Establezca `$CLUSTERNAME` en el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="97638-147">Establezca `$STORAGEACCOUNTNAME` en el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="97638-148">El comando siguiente muestra cómo usar [curl (http://curl.haxx.se/)](http://curl.haxx.se/) y [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) para recuperar y analizar datos JSON.</span><span class="sxs-lookup"><span data-stu-id="97638-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="97638-149">Cuando use este comando, reemplace __CLUSTERNAME__ por el nombre del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="97638-150">Reemplace __PASSWORD__ por la contraseña de inicio de sesión HTTP del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="97638-151">Reemplace __STORAGEACCOUNT__ por el nombre de la cuenta de almacenamiento agregada mediante la acción de script.</span><span class="sxs-lookup"><span data-stu-id="97638-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="97638-152">La información que devuelve este comando es similar al siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="97638-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="97638-153">Este texto es un ejemplo de una clave cifrada que se usa para acceder a la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="97638-154">No se puede acceder a almacenamiento después de cambiar la clave</span><span class="sxs-lookup"><span data-stu-id="97638-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="97638-155">Si cambia la clave de una cuenta de almacenamiento, HDInsight ya no podrá acceder a dicha cuenta.</span><span class="sxs-lookup"><span data-stu-id="97638-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="97638-156">HDInsight usa una copia en caché de clave del archivo core-site.xml para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="97638-157">Esta copia en caché debe actualizarse para que coincida con la nueva.</span><span class="sxs-lookup"><span data-stu-id="97638-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="97638-158">La ejecución nuevamente de la acción de script __no__ actualizará la clave, ya que el script comprueba si ya existe una entrada para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="97638-159">Si ya existe una entrada, no realice ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="97638-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="97638-160">Para solucionar este problema, debe quitar la entrada existente para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97638-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="97638-161">Realice los siguientes pasos para quitar la entrada:</span><span class="sxs-lookup"><span data-stu-id="97638-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="97638-162">Abra un explorador web y abra la interfaz de usuario web de Ambari de su clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="97638-163">El identificador URI es https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="97638-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="97638-164">Reemplace __CLUSTERNAME__ por el nombre del clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="97638-165">Cuando se le solicite, escriba el usuario de inicio de sesión HTTP y la contraseña para el clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="97638-166">En la lista de servicios situada a la izquierda de la página, seleccione __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="97638-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="97638-167">A continuación, seleccione la pestaña __Configs__ (Configuraciones) en el centro de la página.</span><span class="sxs-lookup"><span data-stu-id="97638-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="97638-168">En el campo __Filter...__ (Filtro), escriba un valor de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="97638-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="97638-169">Esta acción devolverá entradas para las cuentas de almacenamiento adicionales que se hayan agregado al clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="97638-170">Hay dos tipos de entradas; __keyprovider__ y __key__.</span><span class="sxs-lookup"><span data-stu-id="97638-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="97638-171">Ambas contendrán el nombre de la cuenta de almacenamiento como parte del nombre de clave.</span><span class="sxs-lookup"><span data-stu-id="97638-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="97638-172">Los siguientes son entradas de ejemplo para una cuenta de almacenamiento denominada __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="97638-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="97638-173">Después de haber identificado las claves de la cuenta de almacenamiento que quiere quitar, use el icono rojo '-' a la derecha de la entrada para eliminarlas.</span><span class="sxs-lookup"><span data-stu-id="97638-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="97638-174">Haga clic en el botón __Guardar__ para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="97638-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="97638-175">Después de guardar los cambios, use la acción de secuencia de comandos para agregar la cuenta de almacenamiento y el nuevo valor de clave a clúster.</span><span class="sxs-lookup"><span data-stu-id="97638-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="97638-176">Rendimiento deficiente</span><span class="sxs-lookup"><span data-stu-id="97638-176">Poor performance</span></span>

<span data-ttu-id="97638-177">Si la cuenta de almacenamiento está en una región distinta a la del clúster de HDInsight, puede que experimente un rendimiento deficiente.</span><span class="sxs-lookup"><span data-stu-id="97638-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="97638-178">Al acceder a los datos en una región diferente, el tráfico de red se envía fuera del centro de datos regional de Azure y en la red pública de Internet, lo que puede producir latencia.</span><span class="sxs-lookup"><span data-stu-id="97638-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="97638-179">No se admite el uso de una cuenta de almacenamiento en una región diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="97638-180">Cargos adicionales</span><span class="sxs-lookup"><span data-stu-id="97638-180">Additional charges</span></span>

<span data-ttu-id="97638-181">Si la cuenta de almacenamiento se encuentra en una región distinta a la del clúster de HDInsight, puede que observe cargos de salida adicionales en su facturación de Azure.</span><span class="sxs-lookup"><span data-stu-id="97638-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="97638-182">Se aplica un cargo de salida cuando los datos salen de un centro de datos regional.</span><span class="sxs-lookup"><span data-stu-id="97638-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="97638-183">Este cargo se aplica incluso si el tráfico va destinado a otro centro de datos de Azure en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="97638-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="97638-184">No se admite el uso de una cuenta de almacenamiento en una región diferente a la del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97638-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97638-185">Next steps</span></span>

<span data-ttu-id="97638-186">En este documento ha aprendido a agregar más cuentas de almacenamiento a un clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="97638-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="97638-187">Para más información sobre las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="97638-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
