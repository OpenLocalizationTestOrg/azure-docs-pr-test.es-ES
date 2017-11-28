---
title: registros de flujo de aaaRead NSG | Documentos de Microsoft
description: "Este artículo muestra cómo registros de flujo NSG tooparse"
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
ms.openlocfilehash: b4f0f64639c7b2a6b4db50e54d15056bfd809e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="read-nsg-flow-logs"></a><span data-ttu-id="3512e-103">Lectura de registros de flujos de NSG</span><span class="sxs-lookup"><span data-stu-id="3512e-103">Read NSG flow logs</span></span>

<span data-ttu-id="3512e-104">Obtenga información acerca de cómo el flujo NSG tooread registrará las entradas con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3512e-104">Learn how tooread NSG flow logs entries with PowerShell.</span></span>

<span data-ttu-id="3512e-105">Los registros de flujos de NSG se almacenan en una cuenta de almacenamiento de [blobs en bloques](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span><span class="sxs-lookup"><span data-stu-id="3512e-105">NSG flow logs are stored in a storage account in [block blobs](/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs.md#about-block-blobs).</span></span> <span data-ttu-id="3512e-106">Los blobs en bloques se componen de bloques más pequeños.</span><span class="sxs-lookup"><span data-stu-id="3512e-106">Block blobs are made up of smaller blocks.</span></span> <span data-ttu-id="3512e-107">Cada registro es un blob en bloques independiente que se genera cada hora.</span><span class="sxs-lookup"><span data-stu-id="3512e-107">Each log is a separate block blob that is generated every hour.</span></span> <span data-ttu-id="3512e-108">Nuevos registros se generan cada hora, registros de Hola se actualizan con las nuevas entradas cada pocos minutos con datos más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-108">New logs are generated every hour, hello logs are updated with new entries every few minutes with hello latest data.</span></span> <span data-ttu-id="3512e-109">En este artículo aprenderá cómo tooread partes de hello fluyen de registros.</span><span class="sxs-lookup"><span data-stu-id="3512e-109">In this article you learn how tooread portions of hello flow logs.</span></span>

## <a name="scenario"></a><span data-ttu-id="3512e-110">Escenario</span><span class="sxs-lookup"><span data-stu-id="3512e-110">Scenario</span></span>

<span data-ttu-id="3512e-111">Hola siguiendo el escenario, tendrá un registro de flujo de ejemplo que se almacena en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3512e-111">In hello following scenario, you have an example flow log that is stored in a storage account.</span></span> <span data-ttu-id="3512e-112">se ejecutar paso a paso cómo selectivamente puede leer los eventos más recientes de hello en los registros de flujo NSG.</span><span class="sxs-lookup"><span data-stu-id="3512e-112">we step through how you can selectively read hello latest events in NSG flow logs.</span></span> <span data-ttu-id="3512e-113">En este artículo se van a usar PowerShell, sin embargo, no sean lenguaje de programación toohello limitado conceptos Hola descritos en hello artículo y tooall aplicables idiomas de hello las API de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3512e-113">In this article we will use PowerShell, however, hello concepts discussed in hello article are not limited toohello programming language and are applicable tooall languages supported by hello Azure Storage APIs</span></span>

## <a name="setup"></a><span data-ttu-id="3512e-114">Configuración</span><span class="sxs-lookup"><span data-stu-id="3512e-114">Setup</span></span>

<span data-ttu-id="3512e-115">Antes de empezar, tiene que tener el registro de flujo de grupo de seguridad de red habilitado en uno o más grupos de seguridad de red de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3512e-115">Before you begin, you must have Network Security Group Flow Logging enabled on one or many Network Security Groups in your account.</span></span> <span data-ttu-id="3512e-116">Para obtener instrucciones acerca de cómo habilitar la seguridad de red de flujo de registros, consulte el artículo siguiente de toohello: [registro tooflow de introducción para grupos de seguridad de red](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3512e-116">For instructions on enabling Network Security flow logs, refer toohello following article: [Introduction tooflow logging for Network Security Groups](network-watcher-nsg-flow-logging-overview.md).</span></span>

## <a name="retrieve-hello-block-list"></a><span data-ttu-id="3512e-117">Recuperar la lista de bloques de Hola</span><span class="sxs-lookup"><span data-stu-id="3512e-117">Retrieve hello block list</span></span>

<span data-ttu-id="3512e-118">Hola siguientes conjuntos de PowerShell las variables de hello necesarios blob y lista de bloques de hello en Hola de registro de hello tooquery flujo NSG [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="3512e-118">hello following PowerShell sets up hello variables needed tooquery hello NSG flow log blob and list hello blocks within hello [CloudBlockBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblockblob?view=azurestorage-8.1.3) block blob.</span></span> <span data-ttu-id="3512e-119">Actualizar Hola script toocontain los valores válidos para su entorno.</span><span class="sxs-lookup"><span data-stu-id="3512e-119">Update hello script toocontain valid values for your environment.</span></span>

```powershell
# hello SubscriptionID toouse
$subscriptionId = "00000000-0000-0000-0000-000000000000"

# Resource group that contains hello Network Security Group
$resourceGroupName = "<resourceGroupName>"

# hello name of hello Network Security Group
$nsgName = "NSGName"

# hello storage account name that contains hello NSG logs
$storageAccountName = "<storageAccountName>" 

# hello date and time for hello log toobe queried, logs are stored in hour intervals.
[datetime]$logtime = "06/16/2017 20:00"

# Retrieve hello primary storage account key tooaccess hello NSG logs
$StorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName).Value[0]

# Setup a new storage context toobe used tooquery hello logs
$ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

# Container name used by NSG flow logs
$ContainerName = "insights-logs-networksecuritygroupflowevent"

# Name of hello blob that contains hello NSG flow log
$BlobName = "resourceId=/SUBSCRIPTIONS/${subscriptionId}/RESOURCEGROUPS/${resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/${nsgName}/y=$($logtime.Year)/m=$(($logtime).ToString("MM"))/d=$(($logtime).ToString("dd"))/h=$(($logtime).ToString("HH"))/m=00/PT1H.json"

# Gets hello storage blog
$Blob = Get-AzureStorageBlob -Context $ctx -Container $ContainerName -Blob $BlobName

# Gets hello block blog of type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from hello storage blob
$CloudBlockBlob = [Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob] $Blob.ICloudBlob

# Stores hello block list in a variable from hello block blob.
$blockList = $CloudBlockBlob.DownloadBlockList()
```

<span data-ttu-id="3512e-120">Hola `$blockList` variable devuelve una lista de bloques de hello en blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-120">hello `$blockList` variable returns a list of hello blocks in hello blob.</span></span> <span data-ttu-id="3512e-121">Cada blob en bloques contiene al menos dos bloques.</span><span class="sxs-lookup"><span data-stu-id="3512e-121">Each block blob contains at least two blocks.</span></span>  <span data-ttu-id="3512e-122">Hola primer bloque tiene una longitud de `21` bytes, este bloque contiene Hola corchetes del registro de hello json de apertura.</span><span class="sxs-lookup"><span data-stu-id="3512e-122">hello first block has a length of `21` bytes, this block contains hello opening brackets of hello json log.</span></span> <span data-ttu-id="3512e-123">es hello corchete de cierre Hello otro bloque y tiene una longitud de `9` bytes.</span><span class="sxs-lookup"><span data-stu-id="3512e-123">hello other block is hello closing brackets and has a length of `9` bytes.</span></span>  <span data-ttu-id="3512e-124">Como puede ver después de registro de ejemplo de Hola tiene siete entradas en él, cada uno de los que se va a una entrada individual.</span><span class="sxs-lookup"><span data-stu-id="3512e-124">As you can see hello following example log has seven entries in it, each being an individual entry.</span></span> <span data-ttu-id="3512e-125">Todas las nuevas entradas de registro de hello se agregan final toohello justo antes de bloque final Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-125">All new entries in hello log are added toohello end right before hello final block.</span></span>

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

## <a name="read-hello-block-blob"></a><span data-ttu-id="3512e-126">Blob en bloques lectura Hola</span><span class="sxs-lookup"><span data-stu-id="3512e-126">Read hello block blob</span></span>

<span data-ttu-id="3512e-127">A continuación, necesitamos hello tooread `$blocklist` tooretrieve variable datos de saludo.</span><span class="sxs-lookup"><span data-stu-id="3512e-127">Next we need tooread hello `$blocklist` variable tooretrieve hello data.</span></span> <span data-ttu-id="3512e-128">En este ejemplo se recorrer en iteración la lista de bloqueo de hello, leer los bytes de Hola de cada bloque y caso de ellos en una matriz.</span><span class="sxs-lookup"><span data-stu-id="3512e-128">In this example we iterate through hello blocklist, read hello bytes from each block and story them in an array.</span></span> <span data-ttu-id="3512e-129">Usamos hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) datos sobre métodos tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-129">We use hello [DownloadRangeToByteArray](/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob.downloadrangetobytearray?view=azurestorage-8.1.3#Microsoft_WindowsAzure_Storage_Blob_CloudBlob_DownloadRangeToByteArray_System_Byte___System_Int32_System_Nullable_System_Int64__System_Nullable_System_Int64__Microsoft_WindowsAzure_Storage_AccessCondition_Microsoft_WindowsAzure_Storage_Blob_BlobRequestOptions_Microsoft_WindowsAzure_Storage_OperationContext_) method tooretrieve hello data.</span></span>

```powershell
# Set hello size of hello byte array toohello largest block
$maxvalue = ($blocklist | measure Length -Maximum).Maximum

# Create an array toostore values in
$valuearray = @()

# Define hello starting index tootrack hello current block being read
$index = 0

# Loop through each block in hello block list
for($i=0; $i -lt $blocklist.count; $i++)
{

# Create a byte array object toostory hello bytes from hello block
$downloadArray = New-Object -TypeName byte[] -ArgumentList $maxvalue

# Download hello data into hello ByteArray, starting with hello current index, for hello number of bytes in hello current block. Index is increased by 3 when reading tooremove preceding comma.
$CloudBlockBlob.DownloadRangeToByteArray($downloadArray,0,$index+3,$($blockList[$i].Length-1)) | Out-Null

# Increment hello index by adding hello current block length toohello previous index
$index = $index + $blockList[$i].Length

# Retrieve hello string from hello byte array

$value = [System.Text.Encoding]::ASCII.GetString($downloadArray)

# Add hello log entry toohello value array
$valuearray += $value
}
```

<span data-ttu-id="3512e-130">Ahora Hola `$valuearray` matriz contiene el valor de cadena de Hola de cada bloque.</span><span class="sxs-lookup"><span data-stu-id="3512e-130">Now hello `$valuearray` array contains hello string value of each block.</span></span> <span data-ttu-id="3512e-131">entrada de hello tooverify, get hello segundo toohello último valor de matriz de hello ejecutando `$valuearray[$valuearray.Length-2]`.</span><span class="sxs-lookup"><span data-stu-id="3512e-131">tooverify hello entry, get hello second toohello last value from hello array by running `$valuearray[$valuearray.Length-2]`.</span></span> <span data-ttu-id="3512e-132">No queremos Hola último valor es simplemente el corchete de cierre Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-132">We do not want hello last value is just hello closing bracket.</span></span>

<span data-ttu-id="3512e-133">resultados de Hola de este valor se muestran en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="3512e-133">hello results of this value are shown in hello following example:</span></span>

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

<span data-ttu-id="3512e-134">Este escenario es un ejemplo de cómo las entradas de tooread de NSG fluyen de registros sin necesidad de registro de tooparse Hola completo.</span><span class="sxs-lookup"><span data-stu-id="3512e-134">This scenario is an example of how tooread entries in NSG flow logs without having tooparse hello entire log.</span></span> <span data-ttu-id="3512e-135">Puede leer las nuevas entradas de registro de hello tal y como se escriben utilizando el identificador de bloque de Hola o al realizar un seguimiento de la longitud de Hola de bloques que se almacena en el blob en bloques Hola.</span><span class="sxs-lookup"><span data-stu-id="3512e-135">You can read new entries in hello log as they are written by using hello block ID or by tracking hello length of blocks stored in hello block blob.</span></span> <span data-ttu-id="3512e-136">Esto le permite tooread solo hello las nuevas entradas.</span><span class="sxs-lookup"><span data-stu-id="3512e-136">This allows you tooread only hello new entries.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3512e-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3512e-137">Next steps</span></span>

<span data-ttu-id="3512e-138">Visite [visualizar registros de flujo de NSG de Monitor de red de Azure con herramientas de código abierto](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn más información acerca de otro tooview formas NSG flujo de registros.</span><span class="sxs-lookup"><span data-stu-id="3512e-138">Visit [visualize Azure Network Watcher NSG flow logs using open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md) toolearn more about other ways tooview NSG flow logs.</span></span>

<span data-ttu-id="3512e-139">toolearn sobre blobs de almacenamiento, visite: [enlaces de almacenamiento de blobs de funciones de Azure](../azure-functions/functions-bindings-storage-blob.md)</span><span class="sxs-lookup"><span data-stu-id="3512e-139">toolearn more about storage blobs visit: [Azure Functions Blob storage bindings](../azure-functions/functions-bindings-storage-blob.md)</span></span>
