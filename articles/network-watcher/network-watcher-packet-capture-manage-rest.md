---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: API de REST | Documentos de Microsoft'
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante la API de REST de Azure"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="65ee2-103">Administración de capturas de paquetes con Azure Network Watcher mediante la API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="65ee2-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="65ee2-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="65ee2-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="65ee2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65ee2-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="65ee2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="65ee2-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="65ee2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="65ee2-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="65ee2-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="65ee2-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="65ee2-109">Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65ee2-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="65ee2-110">Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="65ee2-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="65ee2-111">Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva.</span><span class="sxs-lookup"><span data-stu-id="65ee2-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="65ee2-112">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="65ee2-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="65ee2-113">Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.</span><span class="sxs-lookup"><span data-stu-id="65ee2-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="65ee2-114">En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="65ee2-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="65ee2-115">**Obtención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="65ee2-116">**Listado de capturas de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="65ee2-117">**Consultar el estado de saludo de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="65ee2-118">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="65ee2-119">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="65ee2-120">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="65ee2-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="65ee2-121">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="65ee2-121">Before you begin</span></span>

<span data-ttu-id="65ee2-122">En este escenario, llame a hello toorun de API de Rest de Monitor de red IP flujo comprobar.</span><span class="sxs-lookup"><span data-stu-id="65ee2-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="65ee2-123">ARMclient es la API de REST de hello toocall utilizados mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65ee2-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="65ee2-124">ARMClient se encuentra en Chocolatey en [ARMClient en Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="65ee2-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="65ee2-125">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="65ee2-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="65ee2-126">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="65ee2-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="65ee2-127">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="65ee2-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="65ee2-128">Inicio de sesión con ARMClient</span><span class="sxs-lookup"><span data-stu-id="65ee2-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="65ee2-129">Recuperación de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="65ee2-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="65ee2-130">Ejecutar Hola después tooreturn de secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65ee2-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="65ee2-131">Esta información es necesaria para iniciar una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="65ee2-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="65ee2-132">Hola siguiendo las variables necesidades de código:</span><span class="sxs-lookup"><span data-stu-id="65ee2-132">hello following code needs variables:</span></span>

- <span data-ttu-id="65ee2-133">**Id. de suscripción** -también se puede recuperar el Id. de suscripción de hello con hello **AzureRMSubscription Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="65ee2-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="65ee2-134">**resourceGroupName** : hello nombre de un grupo de recursos que contiene máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="65ee2-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="65ee2-135">Id. de Hola de máquina virtual de Hola se utiliza en el siguiente ejemplo de Hola desde siguiente Hola resultado.</span><span class="sxs-lookup"><span data-stu-id="65ee2-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="65ee2-136">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="65ee2-136">Get a packet capture</span></span>

<span data-ttu-id="65ee2-137">Hello en el ejemplo siguiente se obtiene estado de Hola de una captura de paquete único</span><span class="sxs-lookup"><span data-stu-id="65ee2-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="65ee2-138">Hello respuestas siguientes son ejemplos de una respuesta típica devuelto al consultar el estado de saludo de una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="65ee2-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="65ee2-139">Listado de capturas de paquetes</span><span class="sxs-lookup"><span data-stu-id="65ee2-139">List all packet captures</span></span>

<span data-ttu-id="65ee2-140">Hola siguiente ejemplo obtiene todas las sesiones de captura de paquetes en una región.</span><span class="sxs-lookup"><span data-stu-id="65ee2-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="65ee2-141">Hola respuesta siguiente es un ejemplo de una respuesta típica devuelta al obtener todos los paquetes se captura</span><span class="sxs-lookup"><span data-stu-id="65ee2-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="65ee2-142">Consulta sobre el estado de captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="65ee2-142">Query packet capture status</span></span>

<span data-ttu-id="65ee2-143">Hola siguiente ejemplo obtiene todas las sesiones de captura de paquetes en una región.</span><span class="sxs-lookup"><span data-stu-id="65ee2-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="65ee2-144">Hello respuesta siguiente es un ejemplo de una respuesta típica devuelto al consultar el estado de saludo de una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="65ee2-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="65ee2-145">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="65ee2-145">Start packet capture</span></span>

<span data-ttu-id="65ee2-146">Hola de ejemplo siguiente crea una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65ee2-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="65ee2-147">ejemplo de Hola es tooallow con parámetros para flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="65ee2-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="65ee2-148">Detención de la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="65ee2-148">Stop packet capture</span></span>

<span data-ttu-id="65ee2-149">Hola siguiente ejemplo detiene una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65ee2-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="65ee2-150">ejemplo de Hola es tooallow con parámetros para flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="65ee2-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="65ee2-151">Eliminación de capturas de paquete</span><span class="sxs-lookup"><span data-stu-id="65ee2-151">Delete packet capture</span></span>

<span data-ttu-id="65ee2-152">Hola de ejemplo siguiente elimina una captura de paquetes en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65ee2-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="65ee2-153">ejemplo de Hola es tooallow con parámetros para flexibilidad en la creación de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="65ee2-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="65ee2-154">Eliminar una captura de paquetes no elimina el archivo hello en la cuenta de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="65ee2-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="65ee2-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65ee2-155">Next steps</span></span>

<span data-ttu-id="65ee2-156">Para obtener instrucciones acerca de cómo descargar archivos desde cuentas de almacenamiento de azure, consulte demasiado[Introducción al almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="65ee2-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="65ee2-157">Otra herramienta que se puede utilizar es el Explorador de Storage.</span><span class="sxs-lookup"><span data-stu-id="65ee2-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="65ee2-158">Para obtener más información acerca del explorador de almacenamiento puede encontrarse aquí en hello siguiente vínculo: [Explorador de almacenamiento](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="65ee2-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="65ee2-159">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="65ee2-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













