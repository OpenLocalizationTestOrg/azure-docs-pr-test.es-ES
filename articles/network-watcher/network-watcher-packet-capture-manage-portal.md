---
title: 'captura de paquetes de aaaManage con Monitor de red de Azure: portal de Azure | Documentos de Microsoft'
description: "Esta página explica cómo toomanage Hola característica de captura de paquetes de Monitor de red mediante el portal de Azure"
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
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="cbefd-103">Administrar capturas de paquetes con Monitor de red de Azure mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="cbefd-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="cbefd-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cbefd-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="cbefd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbefd-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="cbefd-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cbefd-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="cbefd-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cbefd-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="cbefd-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="cbefd-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="cbefd-109">Captura de paquetes de Monitor de red le permite toocreate captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbefd-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="cbefd-110">Los filtros se proporcionan para tooensure de sesión de captura de hello que capturar solamente el tráfico de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="cbefd-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="cbefd-111">Captura de paquetes le ayuda a anomalías de la red toodiagnose tanto de forma reactiva y proactiva.</span><span class="sxs-lookup"><span data-stu-id="cbefd-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="cbefd-112">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="cbefd-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="cbefd-113">Al ser capaz de tooremotely capturas de paquetes de desencadenador, esta capacidad reduce la carga de Hola de una captura de paquetes en ejecución en el equipo deseado de hello, que permite ahorrar tiempo y manualmente.</span><span class="sxs-lookup"><span data-stu-id="cbefd-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="cbefd-114">En este artículo le guiará Hola diferentes tareas de administración que están actualmente disponibles para la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="cbefd-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="cbefd-115">**Inicio de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="cbefd-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="cbefd-116">**Detención de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="cbefd-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="cbefd-117">**Eliminación de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="cbefd-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="cbefd-118">**Descarga de una captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="cbefd-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="cbefd-119">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="cbefd-119">Before you begin</span></span>

<span data-ttu-id="cbefd-120">Este artículo se supone que dispone de hello recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cbefd-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="cbefd-121">Una instancia del Monitor de red en la región de Hola que desea toocreate una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="cbefd-122">Una máquina virtual con el paquete de saludo capturar extensión habilitada.</span><span class="sxs-lookup"><span data-stu-id="cbefd-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbefd-123">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="cbefd-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="cbefd-124">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="cbefd-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="cbefd-125">Extensión del agente de captura de paquetes a través del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="cbefd-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="cbefd-126">captura de paquetes de saludo tooinstall agente de máquina virtual a través del portal de hello, navegar por la máquina virtual de tooyour, haga clic en **extensiones** > **agregar** y busque **agente del Monitor de red para Windows**</span><span class="sxs-lookup"><span data-stu-id="cbefd-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Vista del agente][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="cbefd-128">Introducción a la captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-128">Packet Capture overview</span></span>

<span data-ttu-id="cbefd-129">Navegue toohello [portal de Azure](https://portal.azure.com) y haga clic en **red** > **Monitor de red** > **de captura de paquetes**</span><span class="sxs-lookup"><span data-stu-id="cbefd-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="cbefd-130">página de información general de Hello muestra una lista de todos los paquetes que existen independientemente del estado de hello captura.</span><span class="sxs-lookup"><span data-stu-id="cbefd-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="cbefd-131">Captura de paquetes requiere la cuenta de almacenamiento de toohello de conectividad en el puerto 443.</span><span class="sxs-lookup"><span data-stu-id="cbefd-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![Pantalla de introducción a la captura de paquetes][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="cbefd-133">Inicio de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-133">Start a packet capture</span></span>

<span data-ttu-id="cbefd-134">Haga clic en **agregar** toocreate una captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="cbefd-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="cbefd-135">Hola las propiedades que se pueden definir en una captura de paquetes son:</span><span class="sxs-lookup"><span data-stu-id="cbefd-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="cbefd-136">**Configuración principal**</span><span class="sxs-lookup"><span data-stu-id="cbefd-136">**Main settings**</span></span>

- <span data-ttu-id="cbefd-137">**Suscripción** -este valor es la suscripción de Hola que se usa, se necesita una instancia del Monitor de red en cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="cbefd-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="cbefd-138">**Grupo de recursos** -grupo de recursos de Hola de máquina virtual de Hola que se destina.</span><span class="sxs-lookup"><span data-stu-id="cbefd-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="cbefd-139">**Máquina virtual de destino** -Hola máquina que se está ejecutando la captura de paquetes de saludo</span><span class="sxs-lookup"><span data-stu-id="cbefd-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="cbefd-140">**Nombre de la captura de paquetes** -este valor es el nombre de Hola de captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="cbefd-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="cbefd-141">**Configuración de captura**</span><span class="sxs-lookup"><span data-stu-id="cbefd-141">**Capture configuration**</span></span>

- <span data-ttu-id="cbefd-142">**Cuenta de almacenamiento**: determina si la captura de paquetes se guarda en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cbefd-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="cbefd-143">**Archivo** -determina si una captura de paquetes se guarda localmente en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="cbefd-144">**Las cuentas de almacenamiento** -Hola seleccionado captura de paquetes de almacenamiento cuenta toosave hello en.</span><span class="sxs-lookup"><span data-stu-id="cbefd-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="cbefd-145">La ubicación predeterminada es https://{nombre de la cuenta de almacenamiento}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{nombre del grupo de recursos}/providers/microsoft.compute/virtualmachines/{nombre de la máquina virtual}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span><span class="sxs-lookup"><span data-stu-id="cbefd-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="cbefd-146">(Solo se habilita si está seleccionada la opción **Almacenamiento**)</span><span class="sxs-lookup"><span data-stu-id="cbefd-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="cbefd-147">**Ruta de acceso de archivo local** -ruta de acceso local de hello en una captura de paquetes de máquina virtual toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="cbefd-148">(Solo se habilita si está seleccionada la opción **Archivo**).</span><span class="sxs-lookup"><span data-stu-id="cbefd-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="cbefd-149">Se tiene que proporcionar una ruta de acceso válida</span><span class="sxs-lookup"><span data-stu-id="cbefd-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="cbefd-150">**Número máximo de bytes por paquete** -Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco.</span><span class="sxs-lookup"><span data-stu-id="cbefd-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="cbefd-151">**Número máximo de bytes por sesión** : Total número de bytes que se capturan, una vez que se alcanza el valor de hello deja de captura de paquetes de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="cbefd-152">**Límite de tiempo (segundos)** -establece un límite de tiempo para toostop de captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="cbefd-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="cbefd-153">El valor predeterminado es 18 000 segundos.</span><span class="sxs-lookup"><span data-stu-id="cbefd-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="cbefd-154">Actualmente las cuentas de Premium Storage no se admiten para almacenar paquetes de captura.</span><span class="sxs-lookup"><span data-stu-id="cbefd-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="cbefd-155">**Filtrado (opcional)**</span><span class="sxs-lookup"><span data-stu-id="cbefd-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="cbefd-156">**Protocolo** -Hola toofilter de protocolo para la captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="cbefd-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="cbefd-157">los valores disponibles de Hello son TCP, UDP y ninguno.</span><span class="sxs-lookup"><span data-stu-id="cbefd-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="cbefd-158">**La dirección IP local** -este valor filtra toopackets de captura de paquetes de saludo donde la dirección IP local Hola coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="cbefd-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="cbefd-159">**Puerto local** -este valor filtra toopackets de captura de paquetes de saludo donde puerto local Hola coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="cbefd-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="cbefd-160">**Dirección IP remota** -este valor filtra toopackets de captura de paquetes de saludo donde hello remoto IP coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="cbefd-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="cbefd-161">**Puerto remoto** -este valor filtra toopackets de captura de paquetes de saludo donde puerto remoto hello coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="cbefd-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="cbefd-162">Los valores de dirección IP y puerto pueden ser un solo valor, un rango de valores o un conjunto.</span><span class="sxs-lookup"><span data-stu-id="cbefd-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="cbefd-163">(es decir, 80-1024 para el puerto) Puede definir tantos filtros como desee.</span><span class="sxs-lookup"><span data-stu-id="cbefd-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="cbefd-164">Una vez que se rellenan los valores de hello, haga clic en **Aceptar** toocreate captura de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="cbefd-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![Creación de una captura de paquetes][2]

<span data-ttu-id="cbefd-166">Después de establecer el límite de tiempo de hello en captura de paquetes de saludo ha expirado, captura de paquetes de saludo se detendrá y se puedan revisar.</span><span class="sxs-lookup"><span data-stu-id="cbefd-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="cbefd-167">También puede detener manualmente sesiones de capturas de paquetes de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="cbefd-168">Eliminación de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-168">Delete a packet capture</span></span>

<span data-ttu-id="cbefd-169">Paquete de saludo capturar vista, haga clic en hello **menú contextual** (...) o haga clic en y haga clic en **eliminar** captura de paquetes de saludo toostop</span><span class="sxs-lookup"><span data-stu-id="cbefd-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Eliminación de una captura de paquetes][3]

> [!NOTE]
> <span data-ttu-id="cbefd-171">Eliminar una captura de paquetes no elimina archivos hello en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="cbefd-172">Se le pide tooconfirm desea toodelete captura de paquetes de saludo, haga clic en **sí**</span><span class="sxs-lookup"><span data-stu-id="cbefd-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Confirmación][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="cbefd-174">Detención de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-174">Stop a packet capture</span></span>

<span data-ttu-id="cbefd-175">Paquete de saludo capturar vista, haga clic en hello **menú contextual** (...) o haga clic en y haga clic en **detener** captura de paquetes de saludo toostop</span><span class="sxs-lookup"><span data-stu-id="cbefd-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="cbefd-176">Descarga de una captura de paquetes</span><span class="sxs-lookup"><span data-stu-id="cbefd-176">Download a packet capture</span></span>

<span data-ttu-id="cbefd-177">Una vez que haya finalizado la sesión de captura de paquetes, Hola captura archivo es tooblob cargado tooa o almacenamiento local en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbefd-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="cbefd-178">ubicación de almacenamiento de Hola de captura de paquetes de saludo se define en la creación de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbefd-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="cbefd-179">Una herramienta adecuada tooaccess estos capturar los archivos de cuenta de almacenamiento de tooa guardado es Microsoft Azure Storage Explorer, que puede descargarse aquí: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="cbefd-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="cbefd-180">Si se especifica una cuenta de almacenamiento, archivos de captura de paquetes se guardan tooa cuenta de almacenamiento en hello ubicación siguiente:</span><span class="sxs-lookup"><span data-stu-id="cbefd-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="cbefd-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbefd-181">Next steps</span></span>

<span data-ttu-id="cbefd-182">Obtenga información acerca de la captura de paquetes de tooautomate con las alertas de la máquina Virtual mediante la visualización [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="cbefd-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="cbefd-183">Para comprobar si se permite cierto tráfico hacia o desde la máquina virtual, vea cómo [consultar la Comprobación del flujo de IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cbefd-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













