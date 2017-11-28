---
title: "Administración de capturas de paquetes con Azure Network Watcher: CLI de Azure 1.0 | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante la CLI de Azure 1.0"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="14db4-103">Administración de capturas de paquetes con Azure Network Watcher mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="14db4-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="14db4-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="14db4-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="14db4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14db4-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="14db4-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="14db4-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="14db4-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="14db4-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="14db4-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="14db4-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="14db4-109">La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14db4-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="14db4-110">La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea.</span><span class="sxs-lookup"><span data-stu-id="14db4-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="14db4-111">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="14db4-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="14db4-112">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="14db4-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="14db4-113">Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="14db4-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="14db4-114">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="14db4-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="14db4-115">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14db4-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="14db4-116">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="14db4-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="14db4-117">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="14db4-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="14db4-118">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="14db4-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="14db4-119">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="14db4-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="14db4-120">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="14db4-120">Before you begin</span></span>

<span data-ttu-id="14db4-121">En este artículo se da por hecho que tiene los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="14db4-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="14db4-122">Una instancia de Network Watcher en la región donde desea crear una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14db4-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="14db4-123">Una máquina virtual con la extensión de captura de paquetes habilitada.</span><span class="sxs-lookup"><span data-stu-id="14db4-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14db4-124">La captura de paquetes requiere que se esté ejecutando un agente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14db4-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="14db4-125">El agente se instala como una extensión.</span><span class="sxs-lookup"><span data-stu-id="14db4-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="14db4-126">Para más instrucciones acerca de las extensiones de máquina virtual, visite [Características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="14db4-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="14db4-127">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="14db4-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="14db4-128">Paso 1</span><span class="sxs-lookup"><span data-stu-id="14db4-128">Step 1</span></span>

<span data-ttu-id="14db4-129">Ejecute el cmdlet `azure vm extension set` para instalar el agente de captura de paquetes en la máquina virtual invitada.</span><span class="sxs-lookup"><span data-stu-id="14db4-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="14db4-130">En las máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="14db4-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="14db4-131">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="14db4-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="14db4-132">Paso 2</span><span class="sxs-lookup"><span data-stu-id="14db4-132">Step 2</span></span>

<span data-ttu-id="14db4-133">Para asegurarse de que el agente está instalado, ejecute el cmdlet `vm extension get` y pásele el nombre de la máquina virtual y del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="14db4-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="14db4-134">Compruebe la lista resultante para asegurarse de que el agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="14db4-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="14db4-135">El siguiente es un ejemplo de la respuesta de la ejecución de `azure vm extension get`.</span><span class="sxs-lookup"><span data-stu-id="14db4-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="14db4-136">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="14db4-136">Start a packet capture</span></span>

<span data-ttu-id="14db4-137">Una vez completados los pasos anteriores, el agente de captura de paquetes está instalado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14db4-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="14db4-138">Paso 1</span><span class="sxs-lookup"><span data-stu-id="14db4-138">Step 1</span></span>

<span data-ttu-id="14db4-139">El siguiente paso es recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="14db4-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="14db4-140">Esta variable se pasa al cmdlet `network watcher show` en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="14db4-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="14db4-141">Paso 2</span><span class="sxs-lookup"><span data-stu-id="14db4-141">Step 2</span></span>

<span data-ttu-id="14db4-142">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="14db4-142">Retrieve a storage account.</span></span> <span data-ttu-id="14db4-143">Esta cuenta de almacenamiento se utiliza para almacenar el archivo de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14db4-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="14db4-144">Paso 3</span><span class="sxs-lookup"><span data-stu-id="14db4-144">Step 3</span></span>

<span data-ttu-id="14db4-145">Se pueden usar filtros para limitar los datos que se almacenan en la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14db4-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="14db4-146">En el ejemplo siguiente se configura una captura de paquetes con varios filtros.</span><span class="sxs-lookup"><span data-stu-id="14db4-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="14db4-147">Los tres primeros filtros recopilan el tráfico TCP saliente solo de la dirección IP local 10.0.0.3 a los puertos de destino 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="14db4-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="14db4-148">El último filtro recopila solo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="14db4-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="14db4-149">Se pueden definir varios filtros para una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14db4-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="14db4-150">Si se usa una estructura de filtros compleja, es mejor usar filtros como un archivo json para evitar errores de sintaxis.</span><span class="sxs-lookup"><span data-stu-id="14db4-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="14db4-151">Por ejemplo, use el indicador "-r" (en lugar de "-f") y pase la ubicación de un archivo json que contiene los siguientes filtros:</span><span class="sxs-lookup"><span data-stu-id="14db4-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="14db4-152">El ejemplo siguiente es la salida esperada de la ejecución del cmdlet `network watcher packet-capture create`.</span><span class="sxs-lookup"><span data-stu-id="14db4-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="14db4-153">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="14db4-153">Get a packet capture</span></span>

<span data-ttu-id="14db4-154">Al ejecutar el cmdlet `network watcher packet-capture show` se recupera el estado de una captura de paquetes que se está ejecutando o se ha completado.</span><span class="sxs-lookup"><span data-stu-id="14db4-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="14db4-155">El ejemplo siguiente es la salida del cmdlet `network watcher packet-capture show`.</span><span class="sxs-lookup"><span data-stu-id="14db4-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="14db4-156">El ejemplo siguiente es una vez completada la captura.</span><span class="sxs-lookup"><span data-stu-id="14db4-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="14db4-157">El valor de PacketCaptureStatus es Stopped, con un valor de StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="14db4-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="14db4-158">Este valor muestra que la captura de paquetes fue correcta y agotó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="14db4-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="14db4-159">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="14db4-159">Stop a packet capture</span></span>

<span data-ttu-id="14db4-160">Al ejecutar el cmdlet `network watcher packet-capture stop` se detiene una sesión si está en curso.</span><span class="sxs-lookup"><span data-stu-id="14db4-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="14db4-161">El cmdlet no devuelve ninguna respuesta cuando se ejecuta en una sesión de captura actualmente en ejecución o en una sesión que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="14db4-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="14db4-162">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="14db4-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="14db4-163">Eliminar una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="14db4-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="14db4-164">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="14db4-164">Download a packet capture</span></span>

<span data-ttu-id="14db4-165">Una vez finalizada la sesión de captura de paquetes, el archivo de captura se puede cargar en Blob Storage o en un archivo local en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="14db4-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="14db4-166">La ubicación de almacenamiento de la captura de paquetes se define al crear la sesión.</span><span class="sxs-lookup"><span data-stu-id="14db4-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="14db4-167">Una herramienta práctica para acceder a estos archivos de captura guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="14db4-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="14db4-168">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="14db4-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="14db4-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14db4-169">Next steps</span></span>

<span data-ttu-id="14db4-170">Aprenda a automatizar capturas de paquetes con las alertas de máquina virtual en el artículo sobre cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="14db4-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="14db4-171">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="14db4-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
