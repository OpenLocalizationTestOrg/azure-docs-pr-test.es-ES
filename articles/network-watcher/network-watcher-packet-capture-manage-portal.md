---
title: "Administración de capturas de paquetes con Azure Network Watcher: Azure Portal | Microsoft Docs"
description: "En esta página se explica cómo administrar la característica de captura de paquetes de Network Watcher mediante Azure Portal"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 33390532cc4fc1129a4f960d589f41bc95e5a1ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="c0d60-103">Administración de capturas de paquetes con Azure Network Watcher mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c0d60-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c0d60-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d60-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="c0d60-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0d60-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="c0d60-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c0d60-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="c0d60-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c0d60-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="c0d60-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="c0d60-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="c0d60-109">La captura de paquetes de Network Watcher permite crear sesiones de captura para realizar el seguimiento del tráfico hacia y desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d60-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="c0d60-110">La sesión de captura cuenta con filtros para asegurarse de capturar solo el tráfico que se desea.</span><span class="sxs-lookup"><span data-stu-id="c0d60-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="c0d60-111">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="c0d60-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="c0d60-112">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="c0d60-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="c0d60-113">Esta funcionalidad permite desencadenar capturas de paquetes de forma remota, lo que reduce la carga de tener que ejecutar una captura de paquetes manualmente y en el equipo deseado, y permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="c0d60-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="c0d60-114">Este artículo le guiará por las diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="c0d60-115">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="c0d60-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="c0d60-116">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="c0d60-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="c0d60-117">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="c0d60-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="c0d60-118">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="c0d60-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="c0d60-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c0d60-119">Before you begin</span></span>

<span data-ttu-id="c0d60-120">En este artículo se da por hecho que tiene los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c0d60-120">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="c0d60-121">Una instancia de Network Watcher en la región donde desea crear una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="c0d60-122">Una máquina virtual con la extensión de captura de paquetes habilitada.</span><span class="sxs-lookup"><span data-stu-id="c0d60-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d60-123">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="c0d60-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="c0d60-124">Para instalar la extensión en una máquina virtual Windows, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Windows](../virtual-machines/windows/extensions-nwa.md), y en una máquina virtual con Linux, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="c0d60-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="c0d60-125">Extensión del agente de captura de paquetes a través del portal</span><span class="sxs-lookup"><span data-stu-id="c0d60-125">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="c0d60-126">Para instalar el agente de captura de paquetes de máquina virtual a través del portal, vaya a la máquina virtual, haga clic en **Extensiones** > **Agregar** y busque **Agente para Windows de Network Watcher**</span><span class="sxs-lookup"><span data-stu-id="c0d60-126">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Vista del agente][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="c0d60-128">Introducción a la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-128">Packet Capture overview</span></span>

<span data-ttu-id="c0d60-129">Navegue hasta [Azure Portal](https://portal.azure.com) y haga clic en **Redes** > **Network Watcher** > **Captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="c0d60-129">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="c0d60-130">La página de información general muestra una lista de todos los paquetes que existen independientemente de su estado.</span><span class="sxs-lookup"><span data-stu-id="c0d60-130">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d60-131">La captura de paquetes requiere conectividad a la cuenta de almacenamiento a través del puerto 443.</span><span class="sxs-lookup"><span data-stu-id="c0d60-131">Packet capture requires connectivity to the storage account over port 443.</span></span>

![Pantalla de introducción a la captura de paquetes][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="c0d60-133">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-133">Start a packet capture</span></span>

<span data-ttu-id="c0d60-134">Haga clic en **Agregar** para crear una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-134">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="c0d60-135">Las propiedades que se pueden definir en una captura de paquetes son:</span><span class="sxs-lookup"><span data-stu-id="c0d60-135">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="c0d60-136">**Configuración principal**</span><span class="sxs-lookup"><span data-stu-id="c0d60-136">**Main settings**</span></span>

- <span data-ttu-id="c0d60-137">**Suscripción**: este valor es la suscripción que se utiliza, se necesita una instancia de Network Watcher en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="c0d60-137">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="c0d60-138">**Grupo de recursos**: el grupo de recursos de destino de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d60-138">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="c0d60-139">**Máquina virtual de destino**: la máquina virtual que está ejecutando la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-139">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="c0d60-140">**Nombre de la captura de paquetes**: este valor es el nombre de la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-140">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="c0d60-141">**Configuración de captura**</span><span class="sxs-lookup"><span data-stu-id="c0d60-141">**Capture configuration**</span></span>

- <span data-ttu-id="c0d60-142">**Cuenta de almacenamiento**: determina si la captura de paquetes se guarda en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c0d60-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="c0d60-143">**Archivo**: determina si una captura de paquetes se guarda localmente en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d60-143">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="c0d60-144">**Cuentas de almacenamiento**: la cuenta de almacenamiento seleccionada para guardar la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-144">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="c0d60-145">La ubicación predeterminada es https://{nombre de la cuenta de almacenamiento}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{nombre del grupo de recursos}/providers/microsoft.compute/virtualmachines/{nombre de la máquina virtual}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="c0d60-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="c0d60-146">(Solo se habilita si está seleccionada la opción **Almacenamiento**)</span><span class="sxs-lookup"><span data-stu-id="c0d60-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="c0d60-147">**Ruta de acceso de archivo local**: la ruta de acceso local en una máquina virtual para guardar la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-147">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="c0d60-148">(Solo se habilita si está seleccionada la opción **Archivo**).</span><span class="sxs-lookup"><span data-stu-id="c0d60-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="c0d60-149">Se tiene que proporcionar una ruta de acceso válida</span><span class="sxs-lookup"><span data-stu-id="c0d60-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="c0d60-150">**Número máximo de bytes por paquete**: el número de bytes de cada paquete que se captura, si se deja en blanco se capturan todos los bytes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-150">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="c0d60-151">**Número máximo de bytes por sesión**: número total de bytes que se capturan, una vez que se alcanza este valor la captura de paquetes se detiene.</span><span class="sxs-lookup"><span data-stu-id="c0d60-151">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="c0d60-152">**Límite de tiempo (segundos)**: establece un límite de tiempo para detener la captura del paquete.</span><span class="sxs-lookup"><span data-stu-id="c0d60-152">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="c0d60-153">El valor predeterminado es 18 000 segundos.</span><span class="sxs-lookup"><span data-stu-id="c0d60-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d60-154">Actualmente las cuentas de Premium Storage no se admiten para almacenar paquetes de captura.</span><span class="sxs-lookup"><span data-stu-id="c0d60-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="c0d60-155">**Filtrado (opcional)**</span><span class="sxs-lookup"><span data-stu-id="c0d60-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="c0d60-156">**Protocolo**: el protocolo para filtrar la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-156">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="c0d60-157">Los valores disponibles son TCP, UDP y Any (cualquiera).</span><span class="sxs-lookup"><span data-stu-id="c0d60-157">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="c0d60-158">**Dirección IP local**: este valor filtra la captura de paquetes a los paquetes en los que la dirección IP local coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="c0d60-158">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="c0d60-159">**Puerto local**: este valor filtra la captura de paquetes a los paquetes en los que el puerto local coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="c0d60-159">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="c0d60-160">**Dirección IP remota**: este valor filtra la captura de paquetes a los paquetes en los que la dirección IP remota coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="c0d60-160">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="c0d60-161">**Puerto remoto**: este valor filtra la captura de paquetes a los paquetes en los que el puerto remoto coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="c0d60-161">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d60-162">Los valores de dirección IP y puerto pueden ser un solo valor, un rango de valores o un conjunto.</span><span class="sxs-lookup"><span data-stu-id="c0d60-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="c0d60-163">(es decir, 80-1024 para el puerto) Puede definir tantos filtros como desee.</span><span class="sxs-lookup"><span data-stu-id="c0d60-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="c0d60-164">Una vez que se rellenan los valores, haga clic en **Aceptar** para crear la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-164">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![Creación de una captura de paquetes][2]

<span data-ttu-id="c0d60-166">Una vez que haya transcurrido el límite de tiempo establecido en la captura de paquetes, esta se detendrá y se podrá revisar.</span><span class="sxs-lookup"><span data-stu-id="c0d60-166">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="c0d60-167">También puede detener manualmente las sesiones de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="c0d60-167">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="c0d60-168">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-168">Delete a packet capture</span></span>

<span data-ttu-id="c0d60-169">En la vista de captura de paquetes, haga clic en el **menú contextual** (...) o haga clic con el botón derecho y haga clic en **Eliminar** para detener la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-169">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![Eliminación de una captura de paquetes][3]

> [!NOTE]
> <span data-ttu-id="c0d60-171">La eliminación de una captura de paquetes no elimina el archivo en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c0d60-171">Deleting a packet capture does not delete the file in the storage account.</span></span>

<span data-ttu-id="c0d60-172">Se le pide que confirme que desea eliminar la captura de paquetes, haga clic en **Sí**</span><span class="sxs-lookup"><span data-stu-id="c0d60-172">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![Confirmación][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="c0d60-174">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-174">Stop a packet capture</span></span>

<span data-ttu-id="c0d60-175">En la vista de captura de paquetes, haga clic en el **menú contextual** (...) o haga clic con el botón derecho y haga clic en **Detener** para detener la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-175">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="c0d60-176">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="c0d60-176">Download a packet capture</span></span>

<span data-ttu-id="c0d60-177">Una vez finalizada la sesión de captura de paquetes, el archivo de captura se carga en Blob Storage o en un archivo local en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c0d60-177">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="c0d60-178">La ubicación de almacenamiento de la captura de paquetes se define al crear la sesión.</span><span class="sxs-lookup"><span data-stu-id="c0d60-178">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="c0d60-179">Una herramienta práctica para acceder a estos archivos de captura guardados en una cuenta de almacenamiento es el Explorador de Microsoft Azure Storage, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="c0d60-179">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="c0d60-180">Si se especifica una cuenta de almacenamiento, los archivos de captura de paquetes se guardan en una cuenta de almacenamiento en la siguiente ubicación:</span><span class="sxs-lookup"><span data-stu-id="c0d60-180">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="c0d60-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0d60-181">Next steps</span></span>

<span data-ttu-id="c0d60-182">Aprenda a automatizar capturas de paquetes con las alertas de máquina virtual en el artículo sobre cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="c0d60-182">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="c0d60-183">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c0d60-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













