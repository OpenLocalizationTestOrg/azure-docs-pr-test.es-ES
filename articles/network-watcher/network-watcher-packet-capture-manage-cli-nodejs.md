---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: 1.0 de CLI de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante Azure CLI 1.0"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="30632-103">Administración de capturas de paquetes con Azure Network Watcher mediante la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="30632-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="30632-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="30632-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="30632-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="30632-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="30632-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="30632-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="30632-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="30632-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="30632-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="30632-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="30632-109">Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="30632-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="30632-110">Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="30632-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="30632-111">Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva.</span><span class="sxs-lookup"><span data-stu-id="30632-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="30632-112">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="30632-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="30632-113">Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.</span><span class="sxs-lookup"><span data-stu-id="30632-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="30632-114">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="30632-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="30632-115">En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="30632-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="30632-116">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="30632-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="30632-117">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="30632-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="30632-118">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="30632-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="30632-119">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="30632-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="30632-120">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="30632-120">Before you begin</span></span>

<span data-ttu-id="30632-121">En este artículo se supone que tiene Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="30632-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="30632-122">Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="30632-123">Una máquina virtual con el paquete de saludo capturar extensión habilitada.</span><span class="sxs-lookup"><span data-stu-id="30632-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="30632-124">Captura de paquete requiere un toobe de agente que se ejecuta en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="30632-125">Hola agente se instala como una extensión.</span><span class="sxs-lookup"><span data-stu-id="30632-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="30632-126">Para más instrucciones acerca de las extensiones de máquina virtual, visite [Características y extensiones de las máquinas virtuales](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="30632-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="30632-127">Instalación de la extensión de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="30632-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="30632-128">Paso 1</span><span class="sxs-lookup"><span data-stu-id="30632-128">Step 1</span></span>

<span data-ttu-id="30632-129">Ejecute hello `azure vm extension set` agente de captura de paquetes cmdlet tooinstall hello en la máquina virtual de hello invitado.</span><span class="sxs-lookup"><span data-stu-id="30632-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="30632-130">En las máquinas virtuales Windows:</span><span class="sxs-lookup"><span data-stu-id="30632-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="30632-131">En las máquinas virtuales Linux:</span><span class="sxs-lookup"><span data-stu-id="30632-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="30632-132">Paso 2</span><span class="sxs-lookup"><span data-stu-id="30632-132">Step 2</span></span>

<span data-ttu-id="30632-133">tooensure que Hola agente está instalado, ejecute hello `vm extension get` cmdlet y pasarlo a grupo de recursos de Hola y el nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="30632-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="30632-134">Compruebe Hola resultante lista tooensure Hola agente está instalado.</span><span class="sxs-lookup"><span data-stu-id="30632-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="30632-135">Hola según muestra es un ejemplo de respuesta de Hola de ejecución`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="30632-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="30632-136">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-136">Start a packet capture</span></span>

<span data-ttu-id="30632-137">Una vez hello pasos anteriores se completa, agente de captura de paquetes de saludo se instala en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="30632-138">Paso 1</span><span class="sxs-lookup"><span data-stu-id="30632-138">Step 1</span></span>

<span data-ttu-id="30632-139">Hola siguiente paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="30632-140">Esta variable se pasa toohello `network watcher show` cmdlet en el paso 4.</span><span class="sxs-lookup"><span data-stu-id="30632-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="30632-141">Paso 2</span><span class="sxs-lookup"><span data-stu-id="30632-141">Step 2</span></span>

<span data-ttu-id="30632-142">Recupere una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="30632-142">Retrieve a storage account.</span></span> <span data-ttu-id="30632-143">Esta cuenta de almacenamiento es el archivo de captura de paquetes de hello toostore usado.</span><span class="sxs-lookup"><span data-stu-id="30632-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="30632-144">Paso 3</span><span class="sxs-lookup"><span data-stu-id="30632-144">Step 3</span></span>

<span data-ttu-id="30632-145">Los filtros pueden ser datos de Hola de toolimit usado almacenado por captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="30632-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="30632-146">Hello en el ejemplo siguiente se configura una captura de paquetes con varios filtros.</span><span class="sxs-lookup"><span data-stu-id="30632-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="30632-147">Hello en primer lugar tres filtros recopilan el tráfico TCP saliente solo de local IP 10.0.0.3 toodestination puertos 20, 80 y 443.</span><span class="sxs-lookup"><span data-stu-id="30632-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="30632-148">último filtro de Hello recopila sólo el tráfico UDP.</span><span class="sxs-lookup"><span data-stu-id="30632-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="30632-149">Se pueden definir varios filtros para una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="30632-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="30632-150">Si se utiliza una estructura de filtro complejas, es mejor filtros toouse como un errores de sintaxis de json archivo tooavoid.</span><span class="sxs-lookup"><span data-stu-id="30632-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="30632-151">Por ejemplo, usar Hola marca "-r" (en lugar de "-f") y pase Hola ubicación de un archivo json que contiene Hola después de filtros:</span><span class="sxs-lookup"><span data-stu-id="30632-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="30632-152">el ejemplo siguiente se Hello es resultado de hello esperada de la ejecución hello `network watcher packet-capture create` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30632-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="30632-153">Obtención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-153">Get a packet capture</span></span>

<span data-ttu-id="30632-154">Ejecuta hello `network watcher packet-capture show` cmdlet, recupera el estado de saludo de una captura de paquetes que se está ejecutando o se han completado.</span><span class="sxs-lookup"><span data-stu-id="30632-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="30632-155">el ejemplo siguiente se Hello es resultado de hello de hello `network watcher packet-capture show` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30632-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="30632-156">Hello siguiente ejemplo es una vez completada la captura de Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="30632-157">Hola PacketCaptureStatus valor se detiene, con un StopReason de TimeExceeded.</span><span class="sxs-lookup"><span data-stu-id="30632-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="30632-158">Este valor muestra que captura de paquetes de saludo fue correcta y ejecutó su tiempo.</span><span class="sxs-lookup"><span data-stu-id="30632-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="30632-159">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-159">Stop a packet capture</span></span>

<span data-ttu-id="30632-160">Mediante la ejecución de hello `network watcher packet-capture stop` cmdlet, si una sesión de captura está en curso se detiene.</span><span class="sxs-lookup"><span data-stu-id="30632-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="30632-161">Hola cmdlet no devuelve ninguna respuesta cuando se ejecutó en una sesión de captura actualmente en ejecución o una sesión existente que ya se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="30632-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="30632-162">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="30632-163">Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="30632-164">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="30632-164">Download a packet capture</span></span>

<span data-ttu-id="30632-165">Una vez que haya finalizado la sesión de captura de paquetes, archivo de captura de hello puede ser cargado tooblob almacenamiento o tooa archivo local Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="30632-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="30632-166">ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="30632-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="30632-167">Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="30632-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="30632-168">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="30632-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="30632-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="30632-169">Next steps</span></span>

<span data-ttu-id="30632-170">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="30632-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="30632-171">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="30632-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
