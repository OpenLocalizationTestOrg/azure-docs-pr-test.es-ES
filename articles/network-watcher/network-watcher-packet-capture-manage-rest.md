---
title: "Administración de capturas de paquetes con Azure Network Watcher: API de REST | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante la API de REST de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="dfc3c-103">Administración de capturas de paquetes con Azure Network Watcher mediante la API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="dfc3c-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="dfc3c-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="dfc3c-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="dfc3c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfc3c-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="dfc3c-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="dfc3c-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="dfc3c-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dfc3c-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="dfc3c-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="dfc3c-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="dfc3c-109">La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="dfc3c-110">La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="dfc3c-111">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="dfc3c-112">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="dfc3c-113">Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="dfc3c-114">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="dfc3c-115">**Obtención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="dfc3c-116">**Listado de capturas de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="dfc3c-117">**Consulta sobre el estado de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="dfc3c-118">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="dfc3c-119">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="dfc3c-120">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="dfc3c-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="dfc3c-121">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="dfc3c-121">Before you begin</span></span>

<span data-ttu-id="dfc3c-122">En este escenario, puede llamar a la API de REST de Network Watcher para ejecutar la comprobación de flujo de IP.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="dfc3c-123">ARMclient se usa para llamar a la API de REST con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="dfc3c-124">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="dfc3c-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="dfc3c-125">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="dfc3c-126">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="dfc3c-127">Para instalar la extensión en una máquina virtual Windows, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Windows](../virtual-machines/windows/extensions-nwa.md), y en una máquina virtual con Linux, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="dfc3c-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="dfc3c-128">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="dfc3c-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="dfc3c-129">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="dfc3c-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="dfc3c-130">Ejecute el siguiente script para devolver una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="dfc3c-131">Esta información es necesaria para iniciar una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="dfc3c-132">El siguiente código necesita variables:</span><span class="sxs-lookup"><span data-stu-id="dfc3c-132">The following code needs variables:</span></span>

- <span data-ttu-id="dfc3c-133">**subscriptionId**: el identificador de la suscripción también puede recuperarse con el cmdlet **Get-AzureRMSubscription**.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="dfc3c-134">**resourceGroupName**: el nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="dfc3c-135">En la salida siguiente, se usa el id. de la máquina virtual en el ejemplo a continuación.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```


## <a name="get-a-packet-capture"></a><span data-ttu-id="dfc3c-136">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-136">Get a packet capture</span></span>

<span data-ttu-id="dfc3c-137">En el ejemplo siguiente se obtiene el estado de una única captura de paquete</span><span class="sxs-lookup"><span data-stu-id="dfc3c-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="dfc3c-138">Las respuestas siguientes son ejemplos de una típica respuesta devuelta al consultar el estado de una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="dfc3c-139">Listado de capturas de paquetes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-139">List all packet captures</span></span>

<span data-ttu-id="dfc3c-140">En el ejemplo siguiente se obtienen todas las sesiones de captura de paquetes de una región.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="dfc3c-141">La respuesta siguiente es un ejemplo de una respuesta típica devuelta al obtener todas las capturas de paquete</span><span class="sxs-lookup"><span data-stu-id="dfc3c-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="dfc3c-142">Consulta sobre el estado de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-142">Query packet capture status</span></span>

<span data-ttu-id="dfc3c-143">En el ejemplo siguiente se obtienen todas las sesiones de captura de paquetes de una región.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="dfc3c-144">La respuesta siguiente es un ejemplo de una típica respuesta devuelta al consultar el estado de una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="dfc3c-145">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-145">Start packet capture</span></span>

<span data-ttu-id="dfc3c-146">En el ejemplo siguiente se crea una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="dfc3c-147">El ejemplo se parametriza para aportar flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="dfc3c-148">Detención de la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-148">Stop packet capture</span></span>

<span data-ttu-id="dfc3c-149">En el ejemplo siguiente se detiene una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="dfc3c-150">El ejemplo se parametriza para aportar flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="dfc3c-151">Eliminación de capturas de paquete</span><span class="sxs-lookup"><span data-stu-id="dfc3c-151">Delete packet capture</span></span>

<span data-ttu-id="dfc3c-152">En el ejemplo siguiente se elimina una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="dfc3c-153">El ejemplo se parametriza para aportar flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="dfc3c-154">La eliminación de una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc3c-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dfc3c-155">Next steps</span></span>

<span data-ttu-id="dfc3c-156">Para más instrucciones acerca de cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="dfc3c-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="dfc3c-157">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="dfc3c-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="dfc3c-158">Encontrará más información acerca del Explorador de Storage en el siguiente vínculo: [Explorador de Storage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="dfc3c-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="dfc3c-159">Aprenda a automatizar capturas de paquetes con las alertas de máquina virtual en el artículo sobre cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="dfc3c-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













