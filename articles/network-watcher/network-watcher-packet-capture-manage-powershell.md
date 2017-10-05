---
title: "Administración de capturas de paquetes con Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04d82085-c9ea-4ea1-b050-a3dd4960f3aa
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abd3b3641da80ee835fac85b4bde68594449e451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="68e2f-103">Administración de capturas de paquetes con Azure Network Watcher mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="68e2f-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="68e2f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="68e2f-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="68e2f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68e2f-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="68e2f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="68e2f-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="68e2f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="68e2f-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="68e2f-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="68e2f-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="68e2f-109">La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68e2f-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="68e2f-110">La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea.</span><span class="sxs-lookup"><span data-stu-id="68e2f-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="68e2f-111">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="68e2f-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="68e2f-112">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="68e2f-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="68e2f-113">Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="68e2f-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="68e2f-114">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68e2f-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="68e2f-115">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="68e2f-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="68e2f-116">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="68e2f-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="68e2f-117">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="68e2f-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="68e2f-118">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="68e2f-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="68e2f-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="68e2f-119">Before you begin</span></span>

<span data-ttu-id="68e2f-120">En este artículo se da por hecho que tiene los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="68e2f-120">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="68e2f-121">Una instancia de Network Watcher en la región donde desea crear una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68e2f-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>

* <span data-ttu-id="68e2f-122">Una máquina virtual con la extensión de captura de paquetes habilitada.</span><span class="sxs-lookup"><span data-stu-id="68e2f-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68e2f-123">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="68e2f-124">Para instalar la extensión en una máquina virtual Windows, visite [Extensión de máquina virtual del agente de Network Watcher para Windows](../virtual-machines/windows/extensions-nwa.md), y en una máquina virtual Linux, visite [Extensión de máquina virtual del agente de Network Watcher para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="68e2f-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="68e2f-125">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="68e2f-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="68e2f-126">Paso 1</span><span class="sxs-lookup"><span data-stu-id="68e2f-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="68e2f-127">Paso 2</span><span class="sxs-lookup"><span data-stu-id="68e2f-127">Step 2</span></span>

<span data-ttu-id="68e2f-128">En el ejemplo siguiente se recupera la información de extensión necesaria para ejecutar el cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-128">The following example retrieves the extension information needed to run the `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="68e2f-129">Este cmdlet instala el agente de captura de paquetes en la máquina virtual invitada.</span><span class="sxs-lookup"><span data-stu-id="68e2f-129">This cmdlet installs the packet capture agent on the guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="68e2f-130">El cmdlet `Set-AzureRmVMExtension` puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="68e2f-130">The `Set-AzureRmVMExtension` cmdlet may take several minutes to complete.</span></span>

<span data-ttu-id="68e2f-131">En las máquinas virtuales con Windows:</span><span class="sxs-lookup"><span data-stu-id="68e2f-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="68e2f-132">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="68e2f-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="68e2f-133">El ejemplo siguiente es una respuesta correcta después de ejecutar el cmdlet `Set-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-133">The following example is a successful response after running the `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="68e2f-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="68e2f-134">Step 3</span></span>

<span data-ttu-id="68e2f-135">Para asegurarse de que el agente está instalado, ejecute el cmdlet `Get-AzureRmVMExtension` y pásele el nombre de la máquina virtual y el nombre de extensión.</span><span class="sxs-lookup"><span data-stu-id="68e2f-135">To ensure that the agent is installed, run the `Get-AzureRmVMExtension` cmdlet and pass it the virtual machine name and the extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="68e2f-136">El siguiente es un ejemplo de la respuesta de la ejecución de `Get-AzureRmVMExtension`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-136">The following sample is an example of the response from running `Get-AzureRmVMExtension`</span></span>

```
ResourceGroupName       : testrg
VMName                  : testvm1
Name                    : AzureNetworkWatcherExtension
Location                : westcentralus
Etag                    : null
Publisher               : Microsoft.Azure.NetworkWatcher
ExtensionType           : NetworkWatcherAgentWindows
TypeHandlerVersion      : 1.4
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1/
                          extensions/AzureNetworkWatcherExtension
PublicSettings          : 
ProtectedSettings       : 
ProvisioningState       : Succeeded
Statuses                : 
SubStatuses             : 
AutoUpgradeMinorVersion : True
ForceUpdateTag          : 
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="68e2f-137">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="68e2f-137">Start a packet capture</span></span>

<span data-ttu-id="68e2f-138">Una vez completados los pasos anteriores, el agente de captura de paquetes está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68e2f-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="68e2f-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="68e2f-139">Step 1</span></span>

<span data-ttu-id="68e2f-140">El siguiente paso es recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="68e2f-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="68e2f-141">Esta variable se pasa al cmdlet `New-AzureRmNetworkWatcherPacketCapture` en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="68e2f-141">This variable is passed to the `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="68e2f-142">Paso 2</span><span class="sxs-lookup"><span data-stu-id="68e2f-142">Step 2</span></span>

<span data-ttu-id="68e2f-143">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="68e2f-143">Retrieve a storage account.</span></span> <span data-ttu-id="68e2f-144">Esta cuenta de almacenamiento se utiliza para almacenar el archivo de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68e2f-144">This storage account is used to store the packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="68e2f-145">Paso 3</span><span class="sxs-lookup"><span data-stu-id="68e2f-145">Step 3</span></span>

<span data-ttu-id="68e2f-146">Se pueden usar filtros para limitar los datos que se almacenan en la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68e2f-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="68e2f-147">En el ejemplo siguiente se configuran dos filtros.</span><span class="sxs-lookup"><span data-stu-id="68e2f-147">The following example sets up two filters.</span></span>  <span data-ttu-id="68e2f-148">Un filtro recopila el tráfico TCP saliente solo de la dirección IP local 10.0.0.3 a los puertos de destino 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="68e2f-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="68e2f-149">El segundo filtro recopila solo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="68e2f-149">The second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="68e2f-150">Se pueden definir varios filtros para una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="68e2f-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="68e2f-151">Paso 4</span><span class="sxs-lookup"><span data-stu-id="68e2f-151">Step 4</span></span>

<span data-ttu-id="68e2f-152">Ejecute el cmdlet `New-AzureRmNetworkWatcherPacketCapture` para iniciar el proceso de captura de paquetes, pasando los valores necesarios recuperados en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="68e2f-152">Run the `New-AzureRmNetworkWatcherPacketCapture` cmdlet to start the packet capture process, passing the required values retrieved in the preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="68e2f-153">El ejemplo siguiente es la salida esperada de la ejecución del cmdlet `New-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-153">The following example is the expected output from running the `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"3bf27278-8251-4651-9546-c7f369855e4e"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]


```

## <a name="get-a-packet-capture"></a><span data-ttu-id="68e2f-154">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="68e2f-154">Get a packet capture</span></span>

<span data-ttu-id="68e2f-155">Al ejecutar el cmdlet `Get-AzureRmNetworkWatcherPacketCapture` se recupera el estado de una captura de paquetes que se está ejecutando o se ha completado.</span><span class="sxs-lookup"><span data-stu-id="68e2f-155">Running the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="68e2f-156">El ejemplo siguiente es la salida del cmdlet `Get-AzureRmNetworkWatcherPacketCapture`.</span><span class="sxs-lookup"><span data-stu-id="68e2f-156">The following example is the output from the `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="68e2f-157">El ejemplo siguiente es una vez completada la captura.</span><span class="sxs-lookup"><span data-stu-id="68e2f-157">The following example is after the capture is complete.</span></span> <span data-ttu-id="68e2f-158">El valor de PacketCaptureStatus es Stopped, con un valor de StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="68e2f-158">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="68e2f-159">Este valor muestra que la captura de paquetes fue correcta y agotó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="68e2f-159">This value shows that the packet capture was successful and ran its time.</span></span>
```
Name                    : PacketCaptureTest
Id                      : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatcher
                          s/NetworkWatcher_westcentralus/packetCaptures/PacketCaptureTest
Etag                    : W/"4b9a81ed-dc63-472e-869e-96d7166ccb9b"
ProvisioningState       : Succeeded
Target                  : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testvm1
BytesToCapturePerPacket : 0
TotalBytesPerSession    : 1073741824
TimeLimitInSeconds      : 60
StorageLocation         : {
                            "StorageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Storage/storageA
                          ccounts/examplestorage",
                            "StoragePath": "https://examplestorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-00000
                          0000000/resourcegroups/testrg/providers/microsoft.compute/virtualmachines/testvm1/2017/02/01/packetcapture_22_42_48_238.cap"
                          }
Filters                 : [
                            {
                              "Protocol": "TCP",
                              "RemoteIPAddress": "1.1.1.1-255.255.255",
                              "LocalIPAddress": "10.0.0.3",
                              "LocalPort": "1-65535",
                              "RemotePort": "20;80;443"
                            },
                            {
                              "Protocol": "UDP",
                              "RemoteIPAddress": "",
                              "LocalIPAddress": "",
                              "LocalPort": "",
                              "RemotePort": ""
                            }
                          ]
CaptureStartTime        : 2/1/2017 10:43:01 PM
PacketCaptureStatus     : Stopped
StopReason              : TimeExceeded
PacketCaptureError      : []
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="68e2f-160">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="68e2f-160">Stop a packet capture</span></span>

<span data-ttu-id="68e2f-161">Al ejecutar el cmdlet `Stop-AzureRmNetworkWatcherPacketCapture` se detiene una sesión si está en curso.</span><span class="sxs-lookup"><span data-stu-id="68e2f-161">By running the `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="68e2f-162">El cmdlet no devuelve ninguna respuesta cuando se ejecuta en una sesión de captura actualmente en ejecución o en una sesión que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="68e2f-162">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="68e2f-163">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="68e2f-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="68e2f-164">Eliminar una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="68e2f-164">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="68e2f-165">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="68e2f-165">Download a packet capture</span></span>

<span data-ttu-id="68e2f-166">Una vez finalizada la sesión de captura de paquetes, el archivo de captura se puede cargar en Blob Storage o en un archivo local en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68e2f-166">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="68e2f-167">La ubicación de almacenamiento de la captura de paquetes se define al crear la sesión.</span><span class="sxs-lookup"><span data-stu-id="68e2f-167">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="68e2f-168">Una herramienta práctica para acceder a estos archivos de captura guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="68e2f-168">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="68e2f-169">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="68e2f-169">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="68e2f-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="68e2f-170">Next steps</span></span>

<span data-ttu-id="68e2f-171">Para más información acerca de cómo automatizar capturas de paquetes con las alertas de máquina virtual, consulte cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="68e2f-171">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="68e2f-172">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar IP Flow Verify](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="68e2f-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














