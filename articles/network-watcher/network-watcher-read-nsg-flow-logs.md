---
title: Lectura de registros de flujos de NSG | Microsoft Docs
description: "En este artículo se muestra cómo analizar registros de flujos de NSG"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: gwallace
ms.openlocfilehash: 9bb48157b2b8e483e063058f761c3a8f531927f9
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="79835-103">Lectura de registros de flujos de NSG</span><span class="sxs-lookup"><span data-stu-id="79835-103">Read NSG flow logs</span></span>

<span data-ttu-id="79835-104">Aprenda a leer las entradas de los registros de flujos de NSG con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79835-104">Learn how to read NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="79835-105">Los registros de flujos de NSG se almacenan en una cuenta de almacenamiento de [blobs en bloques](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="79835-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="79835-106">Los blobs en bloques se componen de bloques más pequeños.</span><span class="sxs-lookup"><span data-stu-id="79835-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="79835-107">Cada registro es un blob en bloques independiente que se genera cada hora.</span><span class="sxs-lookup"><span data-stu-id="79835-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="79835-108">Cada hora se generan registros nuevos, que se actualizan con entradas nuevas cada pocos minutos con los datos más recientes.</span><span class="sxs-lookup"><span data-stu-id="79835-108">New logs are generated every hour, the logs are updated with new entries every few minutes with the latest data.</span></span> <span data-ttu-id="79835-109">En este artículo aprenderá a leer las secciones de los registros de flujos.</span><span class="sxs-lookup"><span data-stu-id="79835-109">In this article you learn how to read portions of the flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="79835-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="79835-110">Scenario</span></span>

<span data-ttu-id="79835-111">En el siguiente escenario tiene un registro de flujo de ejemplo que se almacena en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="79835-111">In the following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="79835-112">Veremos todos los pasos necesarios para leer de forma selectiva los eventos más recientes de los registros de flujos de NSG.</span><span class="sxs-lookup"><span data-stu-id="79835-112">we step through how you can selectively read the latest events in NSG flow logs.</span></span> <span data-ttu-id="79835-113">En este artículo usaremos PowerShell, aunque los conceptos tratados en él no se limitan al lenguaje de programación y se pueden aplicar a todos los lenguajes admitidos por las API de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="79835-113">In this article we will use PowerShell, however, the concepts discussed in the article are not limited to the programming language and are applicable to all languages supported by the Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="79835-114">Configuración</span><span class="sxs-lookup"><span data-stu-id="79835-114">Setup</span></span>

<span data-ttu-id="79835-115">Antes de empezar, tiene que tener el registro de flujo de grupo de seguridad de red habilitado en uno o más grupos de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="79835-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="79835-116">Para ver instrucciones para habilitar los registros de flujo de grupo de seguridad de red, consulte el artículo siguiente: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md) (Introducción al registro de flujo para grupos de seguridad de red).</span><span class="sxs-lookup"><span data-stu-id="79835-116">For instructions on enabling Network Security flow logs, refer to the following article: [Introduction to flow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-the-block-list"></a><span data-ttu-id="79835-117">Recuperación de la lista de bloques</span><span class="sxs-lookup"><span data-stu-id="79835-117">Retrieve the block list</span></span>

<span data-ttu-id="79835-118">En el siguiente PowerShell se configuran las variables necesarias para consultar el blob del registro de flujos de NSG y mostrar los bloques del blob en bloques [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3).</span><span class="sxs-lookup"><span data-stu-id="79835-118">The following PowerShell sets up the variables needed to query the NSG flow log blob and list the blocks within the [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="79835-119">Actualice el script para que contenga valores válidos para su entorno.</span><span class="sxs-lookup"><span data-stu-id="79835-119">Update the script to contain valid values for your environment.</span></span>

```powershell
# The SubscriptionID to use
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains the Network Security Group
$resourceGroupName = "<resourceGroupName>"

# The name of the Network Security Group
$nsgName = "NSGName"

# The storage account name that contains the NSG logs
$storageAccountName = "<storageAccountName>" 

# The date and time for the log to be queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve the primary storage account key to access the NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context to be used to query the logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of the blob that contains the NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets the storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets the block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from the storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores the block list in a variable from the block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="79835-120">La variable `$blockList` devuelve una lista de los bloques del blob.</span><span class="sxs-lookup"><span data-stu-id="79835-120">The `$blockList` variable returns a list of the blocks in the blob.</span></span> <span data-ttu-id="79835-121">Cada blob en bloques contiene al menos dos bloques.</span><span class="sxs-lookup"><span data-stu-id="79835-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="79835-122">El primer bloque tiene una longitud de `21` bytes. Este bloque contiene los corchetes de apertura del registro de json.</span><span class="sxs-lookup"><span data-stu-id="79835-122">The first block has a length of `21` bytes, this block contains the opening brackets of the json log.</span></span> <span data-ttu-id="79835-123">El otro bloque son los corchetes de cierre y tiene una longitud de `9` bytes.</span><span class="sxs-lookup"><span data-stu-id="79835-123">The other block is the closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="79835-124">Como puede ver, el siguiente registro de ejemplo contiene siete entradas, y cada una de ellas representa una entrada.</span><span class="sxs-lookup"><span data-stu-id="79835-124">As you can see the following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="79835-125">Todas las entradas nuevas del registro se agregan al final, justo antes del bloque final.</span><span class="sxs-lookup"><span data-stu-id="79835-125">All new entries in the log are added to the end right before the final block.</span></span>

```
Name                                         Length Committed
----                                         ------ ---------
ZDk5MTk5N2FkNGE0MmY5MTk5ZWViYjA0YmZhODRhYzY=     21      True
NzQxNDA5MTRhNDUzMGI2M2Y1MDMyOWZlN2QwNDZiYzQ=   2685      True
ODdjM2UyMWY3NzFhZTU3MmVlMmU5MDNlOWEwNWE3YWY=   2586      True
ZDU2MjA3OGQ2ZDU3MjczMWQ4MTRmYWNhYjAzOGJkMTg=   2688      True
ZmM3ZWJjMGQ0ZDA1ODJlOWMyODhlOWE3MDI1MGJhMTc=   2775      True
ZGVkYTc4MzQzNjEyMzlmZWE5MmRiNjc1OWE5OTc0OTQ=   2676      True
ZmY2MjUzYTIwYWIyOGU1OTA2ZDY1OWYzNmY2NmU4ZTY=   2777      True
Mzk1YzQwM2U0ZWY1ZDRhOWFlMTNhYjQ3OGVhYmUzNjk=   2675      True
ZjAyZTliYWE3OTI1YWZmYjFmMWI0MjJhNzMxZTI4MDM=      9      True
```

## <a name="read-the-block-blob"></a><span data-ttu-id="79835-126">Lectura del blob en bloques</span><span class="sxs-lookup"><span data-stu-id="79835-126">Read the block blob</span></span>

<span data-ttu-id="79835-127">A continuación tenemos que leer la variable `$blocklist` para recuperar los datos.</span><span class="sxs-lookup"><span data-stu-id="79835-127">Next we need to read the `$blocklist` variable to retrieve the data.</span></span> <span data-ttu-id="79835-128">En este ejemplo se recorre en iteración la lista de bloques, se leen los bytes de cada bloque y se almacenan en una matriz.</span><span class="sxs-lookup"><span data-stu-id="79835-128">In this example we iterate through the blocklist, read the bytes from each block and story them in an array.</span></span> <span data-ttu-id="79835-129">Para recuperar los datos se usa el método [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_).</span><span class="sxs-lookup"><span data-stu-id="79835-129">We use the [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method to retrieve the data.</span></span>

```powershell
# Set the size of the byte array to the largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array to store values in
$valuearray = @()

# Define the starting index to track the current block being read
$index = 0

# Loop through each block in the block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object to story the bytes from the block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download the data into the ByteArray, starting with the current index, for the number of bytes in the current block. Index is increased by 3 when reading to remove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment the index by adding the current block length to the previous index
$index = $index + $blockList[$i].Length

# Retrieve the string from the byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add the log entry to the value array
$valuearray += $value
}
```

<span data-ttu-id="79835-130">Ahora la matriz `$valuearray` contiene el valor de cadena de cada bloque.</span><span class="sxs-lookup"><span data-stu-id="79835-130">Now the `$valuearray` array contains the string value of each block.</span></span> <span data-ttu-id="79835-131">Para comprobar la entrada, ejecute `$valuearray[$valuearray.Length-2]` para obtener el penúltimo valor de la matriz.</span><span class="sxs-lookup"><span data-stu-id="79835-131">To verify the entry, get the second to the last value from the array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="79835-132">No queremos el último valor, que es el corchete de cierre.</span><span class="sxs-lookup"><span data-stu-id="79835-132">We do not want the last value is just the closing bracket.</span></span>

<span data-ttu-id="79835-133">Los resultados de este valor se muestran en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79835-133">The results of this value are shown in the following example:</span></span>

```json
        {
             "time": "2017-06-16T20:59:43.7340000Z",
             "systemId": "5f4d02d3-a7d0-4ed4-9ce8-c0ae9377951c",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/CONTOSORG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/CONTOSONSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_AllowInternetOutBound","flows":[{"mac":"000D3A18077E","flowTuples":["1497646722,10.0.0.4,168.62.32.14,44904,443,T,O,A","1497646722,10.0.0.4,52.240.48.24,45218,443,T,O,A","1497646725,10.
0.0.4,168.62.32.14,44910,443,T,O,A","1497646725,10.0.0.4,52.240.48.24,45224,443,T,O,A","1497646728,10.0.0.4,168.62.32.14,44916,443,T,O,A","1497646728,10.0.0.4,52.240.48.24,45230,443,T,O,A","1497646732,10.0.0.4,168.62.32.14,44922,443,T,O,A","14976
46732,10.0.0.4,52.240.48.24,45236,443,T,O,A","1497646735,10.0.0.4,168.62.32.14,44928,443,T,O,A","1497646735,10.0.0.4,52.240.48.24,45242,443,T,O,A","1497646738,10.0.0.4,168.62.32.14,44934,443,T,O,A","1497646738,10.0.0.4,52.240.48.24,45248,443,T,O,
A","1497646742,10.0.0.4,168.62.32.14,44942,443,T,O,A","1497646742,10.0.0.4,52.240.48.24,45256,443,T,O,A","1497646745,10.0.0.4,168.62.32.14,44948,443,T,O,A","1497646745,10.0.0.4,52.240.48.24,45262,443,T,O,A","1497646749,10.0.0.4,168.62.32.14,44954
,443,T,O,A","1497646749,10.0.0.4,52.240.48.24,45268,443,T,O,A","1497646753,10.0.0.4,168.62.32.14,44960,443,T,O,A","1497646753,10.0.0.4,52.240.48.24,45274,443,T,O,A","1497646756,10.0.0.4,168.62.32.14,44966,443,T,O,A","1497646756,10.0.0.4,52.240.48
.24,45280,443,T,O,A","1497646759,10.0.0.4,168.62.32.14,44972,443,T,O,A","1497646759,10.0.0.4,52.240.48.24,45286,443,T,O,A","1497646763,10.0.0.4,168.62.32.14,44978,443,T,O,A","1497646763,10.0.0.4,52.240.48.24,45292,443,T,O,A","1497646766,10.0.0.4,
168.62.32.14,44984,443,T,O,A","1497646766,10.0.0.4,52.240.48.24,45298,443,T,O,A","1497646769,10.0.0.4,168.62.32.14,44990,443,T,O,A","1497646769,10.0.0.4,52.240.48.24,45304,443,T,O,A","1497646773,10.0.0.4,168.62.32.14,44996,443,T,O,A","1497646773,
10.0.0.4,52.240.48.24,45310,443,T,O,A","1497646776,10.0.0.4,168.62.32.14,45002,443,T,O,A","1497646776,10.0.0.4,52.240.48.24,45316,443,T,O,A","1497646779,10.0.0.4,168.62.32.14,45008,443,T,O,A","1497646779,10.0.0.4,52.240.48.24,45322,443,T,O,A"]}]}
,{"rule":"DefaultRule_DenyAllInBound","flows":[]},{"rule":"UserRule_ssh-rule","flows":[]},{"rule":"UserRule_web-rule","flows":[{"mac":"000D3A18077E","flowTuples":["1497646738,13.82.225.93,10.0.0.4,1180,80,T,I,A","1497646750,13.82.225.93,10.0.0.4,
1184,80,T,I,A","1497646768,13.82.225.93,10.0.0.4,1181,80,T,I,A","1497646780,13.82.225.93,10.0.0.4,1336,80,T,I,A"]}]}]}
        }
```

<span data-ttu-id="79835-134">Este escenario es un ejemplo de cómo leer las entradas de registros de flujos de NSG sin tener que analizar todo el registro.</span><span class="sxs-lookup"><span data-stu-id="79835-134">This scenario is an example of how to read entries in NSG flow logs without having to parse the entire log.</span></span> <span data-ttu-id="79835-135">Puede leer las entradas nuevas del registro a medida que se escriben mediante el identificador de bloque o mediante el seguimiento de la longitud de los bloques almacenados en el blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="79835-135">You can read new entries in the log as they are written by using the block ID or by tracking the length of blocks stored in the block blob.</span></span> <span data-ttu-id="79835-136">Esto le permite leer solo las entradas nuevas.</span><span class="sxs-lookup"><span data-stu-id="79835-136">This allows you to read only the new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="79835-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="79835-137">Next steps</span></span>

<span data-ttu-id="79835-138">Visite [Visualización de registros de flujo de grupo de seguridad de red de Azure Network Watcher con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) para obtener más información sobre otros métodos para consultar los registros de flujos de NSG.</span><span class="sxs-lookup"><span data-stu-id="79835-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) to learn more about other ways to view NSG flow logs.</span></span>

<span data-ttu-id="79835-139">Para obtener más información sobre los blobs de almacenamiento, visite [Enlaces de Blob Storage en Azure Functions](../azure-functions/functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="79835-139">To learn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>