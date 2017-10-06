---
title: cuentas de almacenamiento de Azure adicional aaaAdd tooHDInsight | Documentos de Microsoft
description: "Obtenga información acerca de cómo las cuentas de almacenamiento de Azure adicionales de tooadd tooan clúster de HDInsight existente."
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="1359d-103">Agregar tooHDInsight de cuentas de almacenamiento adicional</span><span class="sxs-lookup"><span data-stu-id="1359d-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="1359d-104">Obtenga información acerca de cómo las cuentas de tooHDInsight toouse script acciones tooadd adicionales almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="1359d-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="1359d-105">Hello pasos de este documento agregan un clúster de HDInsight basados en Linux existente de almacenamiento cuenta tooan.</span><span class="sxs-lookup"><span data-stu-id="1359d-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1359d-106">información de Hello en este documento es sobre la adición de clúster de almacenamiento adicional tooa después de que se ha creado.</span><span class="sxs-lookup"><span data-stu-id="1359d-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="1359d-107">Para más información sobre cómo agregar cuentas de almacenamiento durante la creación del clúster, consulte [Configuración de clústeres de HDInsight con Hadoop, Spark, Kafka y mucho más](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1359d-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1359d-108">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="1359d-108">How it works</span></span>

<span data-ttu-id="1359d-109">Este script toma Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="1359d-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="1359d-110">__Nombre de la cuenta de almacenamiento de Azure__: nombre de Hola Hola almacenamiento cuenta tooadd toohello del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1359d-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="1359d-111">Después de ejecutar el script de Hola, HDInsight puede leer y escribir datos almacenados en esta cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1359d-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="1359d-112">__Clave de cuenta de almacenamiento de Azure__: una clave que conceda acceso a cuenta de almacenamiento de toohello.</span><span class="sxs-lookup"><span data-stu-id="1359d-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="1359d-113">__-p__ (opcional): si se especifica, clave hello no se cifra y se almacena en el archivo de core-site.xml de hello como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="1359d-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="1359d-114">Durante el procesamiento, el script de Hola realiza Hola siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="1359d-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="1359d-115">Si hello cuenta de almacenamiento ya existe en la configuración de core-site.xml hello para el clúster de hello, Hola script se cerrará y no se llevan a cabo ninguna acción adicional.</span><span class="sxs-lookup"><span data-stu-id="1359d-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="1359d-116">Comprueba que la cuenta de almacenamiento de hello existe y puede tener acceso mediante la clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="1359d-117">Cifra la clave de hello mediante credenciales de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="1359d-118">Agrega el archivo core-site.xml toohello de hello almacenamiento cuenta.</span><span class="sxs-lookup"><span data-stu-id="1359d-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="1359d-119">Detiene y reinicia los servicios de Oozie, YARN, MapReduce2 y HDFS Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="1359d-120">Detener e iniciar estos servicios les permite nueva cuenta de almacenamiento de toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="1359d-121">No se admite el uso de una cuenta de almacenamiento en una ubicación diferente que el clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="1359d-122">script de Hola</span><span class="sxs-lookup"><span data-stu-id="1359d-122">hello script</span></span>

<span data-ttu-id="1359d-123">__Ubicación del script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="1359d-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="1359d-124">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="1359d-124">__Requirements__:</span></span>

* <span data-ttu-id="1359d-125">se debe aplicar el script de Hola en hello __Head nodos__.</span><span class="sxs-lookup"><span data-stu-id="1359d-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="1359d-126">script de Hola toouse</span><span class="sxs-lookup"><span data-stu-id="1359d-126">toouse hello script</span></span>

<span data-ttu-id="1359d-127">Este script puede utilizarse desde Hola portal de Azure, Azure PowerShell, u Hola 1.0 de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1359d-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="1359d-128">Para obtener más información, vea hello [mediante la acción de secuencia de comandos de clústeres de HDInsight basados en Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="1359d-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1359d-129">Al usar pasos de hello indicados en documento de personalización de hello, use Hola después información tooapply esta secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="1359d-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="1359d-130">Reemplace cualquier URI de acción de secuencia de comandos de ejemplo con hello URI para esta secuencia de comandos (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="1359d-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="1359d-131">Reemplace los parámetros de ejemplo por nombre de cuenta de almacenamiento de Azure de Hola y la clave de clúster agregado toohello toobe cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="1359d-132">Si utiliza hello portal de Azure, estos parámetros deben estar separados por un espacio.</span><span class="sxs-lookup"><span data-stu-id="1359d-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="1359d-133">No es necesario toomark esta secuencia de comandos como __Persisted__, tal y como actualiza directamente configuración de Ambari de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="1359d-134">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="1359d-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="1359d-135">Cuentas de almacenamiento que no se muestran en Azure Portal o las herramientas</span><span class="sxs-lookup"><span data-stu-id="1359d-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="1359d-136">Cuando visualización hello HDInsight clúster Hola portal de Azure, seleccionar hello __cuentas de almacenamiento__ entrada bajo __propiedades__ no muestra las cuentas de almacenamiento agregadas a través de esta acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="1359d-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="1359d-137">Azure PowerShell y la CLI de Azure no muestran cuenta de almacenamiento adicional de Hola o.</span><span class="sxs-lookup"><span data-stu-id="1359d-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="1359d-138">no se muestra información de almacenamiento de Hello porque el script de Hola sólo modifica la configuración de core-site.xml de hello para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="1359d-139">Esta información no se utiliza al recuperar la información de clúster de hello mediante las API de administración de Azure.</span><span class="sxs-lookup"><span data-stu-id="1359d-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="1359d-140">información de cuenta de almacenamiento tooview agrega clúster toohello mediante este script, utilice Hola API de REST de Ambari.</span><span class="sxs-lookup"><span data-stu-id="1359d-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="1359d-141">Usar hello después comandos tooretrieve esta información para el clúster:</span><span class="sxs-lookup"><span data-stu-id="1359d-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="1359d-142">Establecer `$clusterName` toohello nombre hello del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1359d-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="1359d-143">Establecer `$storageAccountName` toohello nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="1359d-144">Cuando se le solicite, escriba el inicio de sesión de clúster de hello (admin) y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="1359d-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="1359d-145">Establecer `$PASSWORD` toohello contraseña de la cuenta de inicio de sesión (admin) de clúster.</span><span class="sxs-lookup"><span data-stu-id="1359d-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="1359d-146">Establecer `$CLUSTERNAME` toohello nombre hello del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1359d-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="1359d-147">Establecer `$STORAGEACCOUNTNAME` toohello nombre de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="1359d-148">Este ejemplo se utiliza [curl (http://curl.haxx.se/)](http://curl.haxx.se/) y [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve y analizar datos JSON.</span><span class="sxs-lookup"><span data-stu-id="1359d-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="1359d-149">Si utiliza este comando, reemplace __CLUSTERNAME__ con el nombre de Hola Hola del clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1359d-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="1359d-150">Reemplace __contraseña__ con la contraseña de inicio de sesión de hello HTTP para el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="1359d-151">Reemplace __STORAGEACCOUNT__ con el nombre de Hola de cuenta de almacenamiento de hello agregada mediante la acción de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="1359d-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="1359d-152">Información devuelta por este comando aparece toohello similar siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="1359d-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="1359d-153">Este texto es un ejemplo de una clave cifrada, que se usa tooaccess Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1359d-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="1359d-154">No se puede tooaccess almacenamiento después de cambiar la clave</span><span class="sxs-lookup"><span data-stu-id="1359d-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="1359d-155">Si cambia la clave de Hola para una cuenta de almacenamiento, HDInsight ya no puede acceder a la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="1359d-156">HDInsight utiliza una copia en caché de clave en hello core-site.xml para clúster Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="1359d-157">Esta copia en caché debe ser clave nueva de hello toomatch actualizada.</span><span class="sxs-lookup"><span data-stu-id="1359d-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="1359d-158">Ejecuta la acción de secuencia de comandos de hello nuevo __no__ actualizar la clave de hello, tal y como toosee el script de Hola comprueba si ya existe una entrada para la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="1359d-159">Si ya existe una entrada, no realice ningún cambio.</span><span class="sxs-lookup"><span data-stu-id="1359d-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="1359d-160">toowork solucionar este problema, debe quitar la entrada existente de Hola Hola cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1359d-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="1359d-161">Usar hello siguientes pasos tooremove Hola existente entrada:</span><span class="sxs-lookup"><span data-stu-id="1359d-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="1359d-162">En un explorador web, abra hello Ambari Web UI para el clúster de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1359d-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="1359d-163">Hola URI es https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1359d-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="1359d-164">Reemplace __CLUSTERNAME__ con nombre hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="1359d-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="1359d-165">Cuando se le solicite, escriba Hola HTTP inicio de sesión y la contraseña para el clúster.</span><span class="sxs-lookup"><span data-stu-id="1359d-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="1359d-166">En la lista hello de servicios en la izquierda de Hola de página de hello, seleccione __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="1359d-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="1359d-167">A continuación, seleccione hello __configuraciones__ ficha en el centro de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="1359d-168">Hola __filtro...__  , introduzca un valor de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="1359d-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="1359d-169">Esto devuelve las entradas para las cuentas de almacenamiento adicional que se han agregado toohello clúster.</span><span class="sxs-lookup"><span data-stu-id="1359d-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="1359d-170">Hay dos tipos de entradas; __keyprovider__ y __key__.</span><span class="sxs-lookup"><span data-stu-id="1359d-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="1359d-171">Ambos contienen el nombre hello de cuenta de almacenamiento de hello como parte del nombre de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="1359d-172">Hello siguientes son las entradas de ejemplo para una cuenta de almacenamiento denominada __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="1359d-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="1359d-173">Después de haber identificado las claves de Hola Hola cuenta de almacenamiento necesita tooremove, usar hello rojo '-' toohello icono derecha de hello entrada toodelete lo.</span><span class="sxs-lookup"><span data-stu-id="1359d-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="1359d-174">A continuación, usar hello __guardar__ botón toosave los cambios.</span><span class="sxs-lookup"><span data-stu-id="1359d-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="1359d-175">Una vez que se guardaron los cambios, utilice cuenta de almacenamiento de hello script acción tooadd hello y toohello valor de clave nuevo.</span><span class="sxs-lookup"><span data-stu-id="1359d-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="1359d-176">Rendimiento deficiente</span><span class="sxs-lookup"><span data-stu-id="1359d-176">Poor performance</span></span>

<span data-ttu-id="1359d-177">Si la cuenta de almacenamiento de hello está en una región diferente de clúster de HDInsight de hello, puede experimentar un rendimiento deficiente.</span><span class="sxs-lookup"><span data-stu-id="1359d-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="1359d-178">Acceso a datos de un región diferente envía tráfico de red fuera de centro de datos de Azure regional de Hola y a través Hola internet pública, que puede presentar latencia.</span><span class="sxs-lookup"><span data-stu-id="1359d-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="1359d-179">No se admite el uso de una cuenta de almacenamiento en una región diferente de clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="1359d-180">Cargos adicionales</span><span class="sxs-lookup"><span data-stu-id="1359d-180">Additional charges</span></span>

<span data-ttu-id="1359d-181">Si cuenta de almacenamiento de hello es en una región distinta de Hola clúster de HDInsight, puede que experimente cargos de salida adicionales en la facturación de Azure.</span><span class="sxs-lookup"><span data-stu-id="1359d-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="1359d-182">Se aplica un cargo de salida cuando los datos salen de un centro de datos regional.</span><span class="sxs-lookup"><span data-stu-id="1359d-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="1359d-183">Este cargo se aplica incluso si el tráfico de hello está destinado a otro centro de datos de Azure en una región distinta.</span><span class="sxs-lookup"><span data-stu-id="1359d-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="1359d-184">No se admite el uso de una cuenta de almacenamiento en una región diferente de clúster de HDInsight de Hola.</span><span class="sxs-lookup"><span data-stu-id="1359d-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1359d-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1359d-185">Next steps</span></span>

<span data-ttu-id="1359d-186">Ha aprendido cómo las cuentas de almacenamiento adicional de tooadd tooan clúster de HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="1359d-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="1359d-187">Para más información sobre las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1359d-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
