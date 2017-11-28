---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: PowerShell | Documentos de Microsoft'
description: "Esta página explica cómo la captura de paquete de saludo toomanage característica de Monitor de red con PowerShell"
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
ms.openlocfilehash: 77a522a1b05e020a73ba7140c1410615eb8761da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-powershell"></a><span data-ttu-id="eaf47-103">Administración de capturas de paquetes con Azure Network Watcher mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="eaf47-103">Manage packet captures with Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="eaf47-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="eaf47-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="eaf47-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eaf47-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="eaf47-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eaf47-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="eaf47-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eaf47-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="eaf47-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="eaf47-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="eaf47-109">Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eaf47-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="eaf47-110">Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="eaf47-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="eaf47-111">Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva.</span><span class="sxs-lookup"><span data-stu-id="eaf47-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="eaf47-112">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="eaf47-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="eaf47-113">Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.</span><span class="sxs-lookup"><span data-stu-id="eaf47-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="eaf47-114">En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="eaf47-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="eaf47-115">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="eaf47-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="eaf47-116">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="eaf47-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="eaf47-117">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="eaf47-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="eaf47-118">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="eaf47-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="eaf47-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="eaf47-119">Before you begin</span></span>

<span data-ttu-id="eaf47-120">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="eaf47-120">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="eaf47-121">Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>

* <span data-ttu-id="eaf47-122">Una máquina virtual con el paquete de saludo capturar extensión habilitada.</span><span class="sxs-lookup"><span data-stu-id="eaf47-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eaf47-123">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="eaf47-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="eaf47-124">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="eaf47-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="eaf47-125">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="eaf47-125">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="eaf47-126">Paso 1</span><span class="sxs-lookup"><span data-stu-id="eaf47-126">Step 1</span></span>

```powershell
$VM = Get-AzureRmVM -ResourceGroupName testrg -Name VM1
```

### <a name="step-2"></a><span data-ttu-id="eaf47-127">Paso 2</span><span class="sxs-lookup"><span data-stu-id="eaf47-127">Step 2</span></span>

<span data-ttu-id="eaf47-128">el ejemplo siguiente se recupera información de la extensión de Hola Hola necesarios toorun hello `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eaf47-128">hello following example retrieves hello extension information needed toorun hello `Set-AzureRmVMExtension` cmdlet.</span></span> <span data-ttu-id="eaf47-129">Este cmdlet instala el agente de captura de paquetes de saludo en la máquina virtual de hello invitado.</span><span class="sxs-lookup"><span data-stu-id="eaf47-129">This cmdlet installs hello packet capture agent on hello guest virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf47-130">Hola `Set-AzureRmVMExtension` cmdlet puede tardar varios toocomplete minutos.</span><span class="sxs-lookup"><span data-stu-id="eaf47-130">hello `Set-AzureRmVMExtension` cmdlet may take several minutes toocomplete.</span></span>

<span data-ttu-id="eaf47-131">En las máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="eaf47-131">For Windows virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentWindows -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
```

<span data-ttu-id="eaf47-132">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="eaf47-132">For Linux virtual machines:</span></span>

```powershell
$AzureNetworkWatcherExtension = Get-AzureRmVMExtensionImage -Location WestCentralUS -PublisherName Microsoft.Azure.NetworkWatcher -Type NetworkWatcherAgentLinux -Version 1.4.13.0
$ExtensionName = "AzureNetworkWatcherExtension"
Set-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -Location $VM.Location -VMName $VM.Name -Name $ExtensionName -Publisher $AzureNetworkWatcherExtension.PublisherName -ExtensionType $AzureNetworkWatcherExtension.Type -TypeHandlerVersion $AzureNetworkWatcherExtension.Version.Substring(0,3)
````

<span data-ttu-id="eaf47-133">Hello ejemplo siguiente es una respuesta correcta después de ejecutar hello `Set-AzureRmVMExtension` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eaf47-133">hello following example is a successful response after running hello `Set-AzureRmVMExtension` cmdlet.</span></span>

```
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   
```

### <a name="step-3"></a><span data-ttu-id="eaf47-134">Paso 3</span><span class="sxs-lookup"><span data-stu-id="eaf47-134">Step 3</span></span>

<span data-ttu-id="eaf47-135">tooensure que Hola agente está instalado, ejecute hello `Get-AzureRmVMExtension` cmdlet y pasarlo a nombre de la máquina virtual de Hola y el nombre de la extensión de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-135">tooensure that hello agent is installed, run hello `Get-AzureRmVMExtension` cmdlet and pass it hello virtual machine name and hello extension name.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName $VM.ResourceGroupName  -VMName $VM.Name -Name $ExtensionName
```

<span data-ttu-id="eaf47-136">Hola según muestra es un ejemplo de respuesta de Hola de ejecución`Get-AzureRmVMExtension`</span><span class="sxs-lookup"><span data-stu-id="eaf47-136">hello following sample is an example of hello response from running `Get-AzureRmVMExtension`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="eaf47-137">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-137">Start a packet capture</span></span>

<span data-ttu-id="eaf47-138">Una vez hello pasos anteriores se completa, agente de captura de paquetes de saludo se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="eaf47-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="eaf47-139">Step 1</span></span>

<span data-ttu-id="eaf47-140">Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="eaf47-141">Esta variable se pasa toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="eaf47-141">This variable is passed toohello `New-AzureRmNetworkWatcherPacketCapture` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName  
```

### <a name="step-2"></a><span data-ttu-id="eaf47-142">Paso 2</span><span class="sxs-lookup"><span data-stu-id="eaf47-142">Step 2</span></span>

<span data-ttu-id="eaf47-143">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eaf47-143">Retrieve a storage account.</span></span> <span data-ttu-id="eaf47-144">Esta cuenta de almacenamiento es el archivo de captura de paquetes de hello toostore usado.</span><span class="sxs-lookup"><span data-stu-id="eaf47-144">This storage account is used toostore hello packet capture file.</span></span>

```powershell
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName testrg -Name testrgsa123
```

### <a name="step-3"></a><span data-ttu-id="eaf47-145">Paso 3</span><span class="sxs-lookup"><span data-stu-id="eaf47-145">Step 3</span></span>

<span data-ttu-id="eaf47-146">Los filtros pueden ser datos de Hola de toolimit usado almacenado por captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="eaf47-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="eaf47-147">Hello en el ejemplo siguiente se configura dos filtros.</span><span class="sxs-lookup"><span data-stu-id="eaf47-147">hello following example sets up two filters.</span></span>  <span data-ttu-id="eaf47-148">Recopila un filtro saliente TCP tráfico solo desde IP local 10.0.0.3 toodestination puertos 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="eaf47-148">One filter collects outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="eaf47-149">segundo filtro de Hello recopila sólo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="eaf47-149">hello second filter collects only UDP traffic.</span></span>

```powershell
$filter1 = New-AzureRmPacketCaptureFilterConfig -Protocol TCP -RemoteIPAddress "1.1.1.1-255.255.255" -LocalIPAddress "10.0.0.3" -LocalPort "1-65535" -RemotePort "20;80;443"
$filter2 = New-AzureRmPacketCaptureFilterConfig -Protocol UDP
```

> [!NOTE]
> <span data-ttu-id="eaf47-150">Se pueden definir varios filtros para una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="eaf47-150">Multiple filters can be defined for a packet capture.</span></span>

### <a name="step-4"></a><span data-ttu-id="eaf47-151">Paso 4</span><span class="sxs-lookup"><span data-stu-id="eaf47-151">Step 4</span></span>

<span data-ttu-id="eaf47-152">Ejecute hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart Hola paquete proceso de captura, pasar valores de hello necesario recuperados Hola pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="eaf47-152">Run hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet toostart hello packet capture process, passing hello required values retrieved in hello preceding steps.</span></span>
```powershell

New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $vm.Id -PacketCaptureName "PacketCaptureTest" -StorageAccountId $storageAccount.id -TimeLimitInSeconds 60 -Filters $filter1, $filter2
```

<span data-ttu-id="eaf47-153">el ejemplo siguiente se Hello es resultado de hello esperada de la ejecución hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eaf47-153">hello following example is hello expected output from running hello `New-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="eaf47-154">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-154">Get a packet capture</span></span>

<span data-ttu-id="eaf47-155">Ejecuta hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, recupera el estado de saludo de una captura de paquetes que se está ejecutando o se han completado.</span><span class="sxs-lookup"><span data-stu-id="eaf47-155">Running hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```powershell
Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

<span data-ttu-id="eaf47-156">el ejemplo siguiente se Hello es resultado de hello de hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eaf47-156">hello following example is hello output from hello `Get-AzureRmNetworkWatcherPacketCapture` cmdlet.</span></span> <span data-ttu-id="eaf47-157">Hello siguiente ejemplo es una vez completada la captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-157">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="eaf47-158">Hola PacketCaptureStatus valor se detiene, con un StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="eaf47-158">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="eaf47-159">Este valor muestra que captura de paquetes de saludo fue correcta y ejecutó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="eaf47-159">This value shows that hello packet capture was successful and ran its time.</span></span>
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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="eaf47-160">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-160">Stop a packet capture</span></span>

<span data-ttu-id="eaf47-161">Mediante la ejecución de hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, si una sesión de captura está en curso se detiene.</span><span class="sxs-lookup"><span data-stu-id="eaf47-161">By running hello `Stop-AzureRmNetworkWatcherPacketCapture` cmdlet, if a capture session is in progress it is stopped.</span></span>

```powershell
Stop-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="eaf47-162">Hola cmdlet no devuelve ninguna respuesta cuando se ejecutó en una sesión de captura actualmente en ejecución o una sesión existente que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="eaf47-162">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="eaf47-163">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-163">Delete a packet capture</span></span>

```powershell
Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName "PacketCaptureTest"
```

> [!NOTE]
> <span data-ttu-id="eaf47-164">Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-164">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="eaf47-165">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="eaf47-165">Download a packet capture</span></span>

<span data-ttu-id="eaf47-166">Una vez que haya finalizado la sesión de captura de paquetes, archivo de captura de hello puede ser cargado tooblob almacenamiento o tooa archivo local Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eaf47-166">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="eaf47-167">ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaf47-167">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="eaf47-168">Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="eaf47-168">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="eaf47-169">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="eaf47-169">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="eaf47-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eaf47-170">Next steps</span></span>

<span data-ttu-id="eaf47-171">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="eaf47-171">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="eaf47-172">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar IP Flow Verify](network-watcher-check-ip-flow-verify-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eaf47-172">Find if certain traffic is allowed in orr out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














