---
title: "Administración de capturas de paquetes con Azure Network Watcher: CLI de Azure 2.0 | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante la CLI de Azure 2.0"
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
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="97cb8-103">Administración de capturas de paquetes con Azure Network Watcher mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="97cb8-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="97cb8-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="97cb8-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="97cb8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97cb8-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="97cb8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97cb8-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="97cb8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="97cb8-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="97cb8-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="97cb8-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="97cb8-109">La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97cb8-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="97cb8-110">La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea.</span><span class="sxs-lookup"><span data-stu-id="97cb8-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="97cb8-111">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="97cb8-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="97cb8-112">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="97cb8-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="97cb8-113">Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="97cb8-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="97cb8-114">En este artículo se usa la CLI de próxima generación para el modelo de implementación de Resource Manager, la CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="97cb8-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="97cb8-115">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="97cb8-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="97cb8-116">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="97cb8-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="97cb8-117">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="97cb8-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="97cb8-118">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="97cb8-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="97cb8-119">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="97cb8-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="97cb8-120">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="97cb8-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="97cb8-121">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="97cb8-121">Before you begin</span></span>

<span data-ttu-id="97cb8-122">En este artículo se da por hecho que tiene los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="97cb8-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="97cb8-123">Una instancia de Network Watcher en la región donde desea crear una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="97cb8-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="97cb8-124">Una máquina virtual con la extensión de captura de paquetes habilitada.</span><span class="sxs-lookup"><span data-stu-id="97cb8-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97cb8-125">La captura de paquetes requiere que se esté ejecutando un agente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97cb8-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="97cb8-126">El agente se instala como una extensión.</span><span class="sxs-lookup"><span data-stu-id="97cb8-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="97cb8-127">Para más instrucciones acerca de las extensiones de máquina virtual, visite [Características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="97cb8-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="97cb8-128">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="97cb8-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="97cb8-129">Paso 1</span><span class="sxs-lookup"><span data-stu-id="97cb8-129">Step 1</span></span>

<span data-ttu-id="97cb8-130">Ejecute el cmdlet `az vm extension set` para instalar el agente de captura de paquetes en la máquina virtual invitada.</span><span class="sxs-lookup"><span data-stu-id="97cb8-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="97cb8-131">En las máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="97cb8-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="97cb8-132">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="97cb8-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="97cb8-133">Paso 2</span><span class="sxs-lookup"><span data-stu-id="97cb8-133">Step 2</span></span>

<span data-ttu-id="97cb8-134">Para asegurarse de que el agente está instalado, ejecute el cmdlet `vm extension get` y pásele el nombre de la máquina virtual y del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="97cb8-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="97cb8-135">Compruebe la lista resultante para asegurarse de que el agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="97cb8-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="97cb8-136">El siguiente es un ejemplo de la respuesta de la ejecución de `az vm extension show`.</span><span class="sxs-lookup"><span data-stu-id="97cb8-136">The following sample is an example of the response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="97cb8-137">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="97cb8-137">Start a packet capture</span></span>

<span data-ttu-id="97cb8-138">Una vez completados los pasos anteriores, el agente de captura de paquetes está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97cb8-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="97cb8-139">Paso 1</span><span class="sxs-lookup"><span data-stu-id="97cb8-139">Step 1</span></span>

<span data-ttu-id="97cb8-140">El siguiente paso es recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="97cb8-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="97cb8-141">El nombre de la instancia de Network Watcher se pasa al cmdlet `az network watcher show` en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="97cb8-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="97cb8-142">Paso 2</span><span class="sxs-lookup"><span data-stu-id="97cb8-142">Step 2</span></span>

<span data-ttu-id="97cb8-143">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97cb8-143">Retrieve a storage account.</span></span> <span data-ttu-id="97cb8-144">Esta cuenta de almacenamiento se utiliza para almacenar el archivo de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="97cb8-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="97cb8-145">Paso 3</span><span class="sxs-lookup"><span data-stu-id="97cb8-145">Step 3</span></span>

<span data-ttu-id="97cb8-146">Se pueden usar filtros para limitar los datos que se almacenan en la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="97cb8-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="97cb8-147">En el ejemplo siguiente se configura una captura de paquetes con varios filtros.</span><span class="sxs-lookup"><span data-stu-id="97cb8-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="97cb8-148">Los tres primeros filtros recopilan el tráfico TCP saliente solo de la dirección IP local 10.0.0.3 a los puertos de destino 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="97cb8-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="97cb8-149">El último filtro recopila solo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="97cb8-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="97cb8-150">El ejemplo siguiente es la salida esperada de la ejecución del cmdlet `az network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="97cb8-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="97cb8-151">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="97cb8-151">Get a packet capture</span></span>

<span data-ttu-id="97cb8-152">Al ejecutar el cmdlet `az network watcher packet-capture show` se recupera el estado de una captura de paquetes que se está ejecutando o se ha completado.</span><span class="sxs-lookup"><span data-stu-id="97cb8-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="97cb8-153">El ejemplo siguiente es la salida del cmdlet `az network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="97cb8-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="97cb8-154">El ejemplo siguiente es una vez completada la captura.</span><span class="sxs-lookup"><span data-stu-id="97cb8-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="97cb8-155">El valor de PacketCaptureStatus es Stopped, con un valor de StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="97cb8-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="97cb8-156">Este valor muestra que la captura de paquetes fue correcta y agotó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="97cb8-156">This value shows that the packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="97cb8-157">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="97cb8-157">Stop a packet capture</span></span>

<span data-ttu-id="97cb8-158">Al ejecutar el cmdlet `az network watcher packet-capture stop` se detiene una sesión si está en curso.</span><span class="sxs-lookup"><span data-stu-id="97cb8-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="97cb8-159">El cmdlet no devuelve ninguna respuesta cuando se ejecuta en una sesión de captura actualmente en ejecución o en una sesión que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="97cb8-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="97cb8-160">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="97cb8-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="97cb8-161">Eliminar una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="97cb8-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="97cb8-162">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="97cb8-162">Download a packet capture</span></span>

<span data-ttu-id="97cb8-163">Una vez finalizada la sesión de captura de paquetes, el archivo de captura se puede cargar en Blob Storage o en un archivo local en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97cb8-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="97cb8-164">La ubicación de almacenamiento de la captura de paquetes se define al crear la sesión.</span><span class="sxs-lookup"><span data-stu-id="97cb8-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="97cb8-165">Una herramienta práctica para acceder a estos archivos de captura guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="97cb8-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="97cb8-166">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="97cb8-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="97cb8-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97cb8-167">Next steps</span></span>

<span data-ttu-id="97cb8-168">Aprenda a automatizar capturas de paquetes con las alertas de máquina virtual en el artículo sobre cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="97cb8-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="97cb8-169">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="97cb8-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
