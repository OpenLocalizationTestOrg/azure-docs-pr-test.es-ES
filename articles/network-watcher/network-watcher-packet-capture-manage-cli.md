---
title: captura de paquetes de aaaManage con Monitor de red de Azure - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante Azure CLI 2.0"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="387f2-103">Administración de capturas de paquetes con Azure Network Watcher mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="387f2-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="387f2-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="387f2-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="387f2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="387f2-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="387f2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="387f2-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="387f2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="387f2-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="387f2-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="387f2-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="387f2-109">Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="387f2-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="387f2-110">Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="387f2-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="387f2-111">Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva.</span><span class="sxs-lookup"><span data-stu-id="387f2-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="387f2-112">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="387f2-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="387f2-113">Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.</span><span class="sxs-lookup"><span data-stu-id="387f2-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="387f2-114">En este artículo usa la CLI de próxima generación para el modelo de implementación de administración de recursos hello, CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="387f2-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="387f2-115">Hola tooperform los pasos de este artículo, deberá demasiado[instalar Hola interfaz de línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="387f2-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="387f2-116">En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="387f2-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="387f2-117">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="387f2-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="387f2-118">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="387f2-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="387f2-119">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="387f2-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="387f2-120">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="387f2-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="387f2-121">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="387f2-121">Before you begin</span></span>

<span data-ttu-id="387f2-122">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="387f2-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="387f2-123">Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="387f2-124">Una máquina virtual con el paquete de saludo capturar extensión habilitada.</span><span class="sxs-lookup"><span data-stu-id="387f2-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="387f2-125">Captura de paquete requiere un toobe de agente que se ejecuta en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="387f2-126">Hola agente se instala como una extensión.</span><span class="sxs-lookup"><span data-stu-id="387f2-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="387f2-127">Para más instrucciones acerca de las extensiones de máquina virtual, visite [Características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="387f2-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="387f2-128">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="387f2-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="387f2-129">Paso 1</span><span class="sxs-lookup"><span data-stu-id="387f2-129">Step 1</span></span>

<span data-ttu-id="387f2-130">Ejecute hello `az vm extension set` agente de captura de paquetes cmdlet tooinstall hello en la máquina virtual de hello invitado.</span><span class="sxs-lookup"><span data-stu-id="387f2-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="387f2-131">En las máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="387f2-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="387f2-132">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="387f2-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="387f2-133">Paso 2</span><span class="sxs-lookup"><span data-stu-id="387f2-133">Step 2</span></span>

<span data-ttu-id="387f2-134">tooensure que Hola agente está instalado, ejecute hello `vm extension get` cmdlet y pasarlo a grupo de recursos de Hola y el nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="387f2-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="387f2-135">Compruebe Hola resultante lista tooensure Hola agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="387f2-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="387f2-136">Hola según muestra es un ejemplo de respuesta de Hola de ejecución`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="387f2-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="387f2-137">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-137">Start a packet capture</span></span>

<span data-ttu-id="387f2-138">Una vez hello pasos anteriores se completa, agente de captura de paquetes de saludo se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="387f2-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="387f2-139">Step 1</span></span>

<span data-ttu-id="387f2-140">Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="387f2-141">Nombre de sección de hello Monitor de red se pasa toohello `az network watcher show` cmdlet en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="387f2-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="387f2-142">Paso 2</span><span class="sxs-lookup"><span data-stu-id="387f2-142">Step 2</span></span>

<span data-ttu-id="387f2-143">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="387f2-143">Retrieve a storage account.</span></span> <span data-ttu-id="387f2-144">Esta cuenta de almacenamiento es el archivo de captura de paquetes de hello toostore usado.</span><span class="sxs-lookup"><span data-stu-id="387f2-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="387f2-145">Paso 3</span><span class="sxs-lookup"><span data-stu-id="387f2-145">Step 3</span></span>

<span data-ttu-id="387f2-146">Los filtros pueden ser datos de Hola de toolimit usado almacenado por captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="387f2-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="387f2-147">Hello en el ejemplo siguiente se configura una captura de paquetes con varios filtros.</span><span class="sxs-lookup"><span data-stu-id="387f2-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="387f2-148">Hello en primer lugar tres filtros recopilan el tráfico TCP saliente solo de local IP 10.0.0.3 toodestination puertos 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="387f2-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="387f2-149">último filtro de Hello recopila sólo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="387f2-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="387f2-150">el ejemplo siguiente se Hello es resultado de hello esperada de la ejecución hello `az network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="387f2-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="387f2-151">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-151">Get a packet capture</span></span>

<span data-ttu-id="387f2-152">Ejecuta hello `az network watcher packet-capture show` cmdlet, recupera el estado de saludo de una captura de paquetes que se está ejecutando o se han completado.</span><span class="sxs-lookup"><span data-stu-id="387f2-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="387f2-153">el ejemplo siguiente se Hello es resultado de hello de hello `az network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="387f2-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="387f2-154">Hello siguiente ejemplo es una vez completada la captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="387f2-155">Hola PacketCaptureStatus valor se detiene, con un StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="387f2-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="387f2-156">Este valor muestra que captura de paquetes de saludo fue correcta y ejecutó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="387f2-156">This value shows that hello packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="387f2-157">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-157">Stop a packet capture</span></span>

<span data-ttu-id="387f2-158">Mediante la ejecución de hello `az network watcher packet-capture stop` cmdlet, si una sesión de captura está en curso se detiene.</span><span class="sxs-lookup"><span data-stu-id="387f2-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="387f2-159">Hola cmdlet no devuelve ninguna respuesta cuando se ejecutó en una sesión de captura actualmente en ejecución o una sesión existente que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="387f2-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="387f2-160">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="387f2-161">Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="387f2-162">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="387f2-162">Download a packet capture</span></span>

<span data-ttu-id="387f2-163">Una vez que haya finalizado la sesión de captura de paquetes, archivo de captura de hello puede ser cargado tooblob almacenamiento o tooa archivo local Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="387f2-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="387f2-164">ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="387f2-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="387f2-165">Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="387f2-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="387f2-166">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="387f2-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="387f2-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="387f2-167">Next steps</span></span>

<span data-ttu-id="387f2-168">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="387f2-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="387f2-169">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="387f2-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
