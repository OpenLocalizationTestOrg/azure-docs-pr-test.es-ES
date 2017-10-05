---
title: "Introducción a la captura de paquetes en Azure Network Watcher | Microsoft Docs"
description: "En esta página se proporciona una información general sobre las funcionalidades de la captura de paquetes de Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="eb0ea-103">Introducción a la captura de paquetes variable en Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="eb0ea-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="eb0ea-104">La captura variable de paquetes de Network Watcher permite crear sesiones de captura de paquetes para realizar el seguimiento del tráfico de entrada y salida de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="eb0ea-105">La captura de paquetes ayuda a diagnosticar anomalías de la red, tanto de forma activa como reactiva.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="eb0ea-106">Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="eb0ea-107">La captura de paquetes es una extensión de máquina virtual que se inicia de forma remota a través de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="eb0ea-108">Esta funcionalidad reduce la carga de la ejecución manual de una captura de paquetes en el equipo deseado, lo que permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="eb0ea-109">La captura de paquetes puede realizarse a través del portal, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="eb0ea-110">Un ejemplo de cómo se puede activar la captura de paquetes es con las alertas de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="eb0ea-111">La sesión de captura cuenta con filtros para asegurar la captura del tráfico que se desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="eb0ea-112">Los filtros se basan en la información de 5-tupla (protocolo, dirección IP local, dirección IP remota, el puerto local y puerto remoto).</span><span class="sxs-lookup"><span data-stu-id="eb0ea-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="eb0ea-113">Los datos capturados se almacenan en el disco local o en un blob de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="eb0ea-114">Hay un límite de 10 sesiones de captura de paquetes por región y suscripción.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="eb0ea-115">Este límite se aplica solo a las sesiones y no a los archivos de captura de paquetes guardados localmente, en la máquina virtual, o en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eb0ea-116">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="eb0ea-117">Para instalar la extensión en una máquina virtual Windows, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Windows](../virtual-machines/windows/extensions-nwa.md), y en una máquina virtual con Linux, consulte [Extensión de máquina virtual del agente de Azure Network Watcher para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="eb0ea-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="eb0ea-118">Para reducir la información que se captura únicamente a la información que desee, las siguientes opciones están disponibles para una sesión de captura de paquetes:</span><span class="sxs-lookup"><span data-stu-id="eb0ea-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="eb0ea-119">**Configuración de captura**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-119">**Capture configuration**</span></span>

|<span data-ttu-id="eb0ea-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="eb0ea-120">Property</span></span>|<span data-ttu-id="eb0ea-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="eb0ea-121">Description</span></span>|
|---|---|
|<span data-ttu-id="eb0ea-122">**Número máximo de bytes por paquete (bytes)**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="eb0ea-123">El número de bytes de cada paquete que se captura, si se deja en blanco se capturan todos los bytes.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="eb0ea-124">El número de bytes de cada paquete que se captura, si se deja en blanco se capturan todos los bytes.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="eb0ea-125">Si necesita solo el encabezado de IPv4, indique 34 aquí</span><span class="sxs-lookup"><span data-stu-id="eb0ea-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="eb0ea-126">**Número máximo de bytes por sesión (bytes)**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="eb0ea-127">Número total de bytes en esa captura, una vez que se alcanza este valor la sesión se finaliza.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="eb0ea-128">**Límite de tiempo (segundos)**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="eb0ea-129">Establece una restricción horaria en la sesión de captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="eb0ea-130">El valor predeterminado es 18000 segundos o 5 horas.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="eb0ea-131">**Filtrado (opcional)**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="eb0ea-132">Propiedad</span><span class="sxs-lookup"><span data-stu-id="eb0ea-132">Property</span></span>|<span data-ttu-id="eb0ea-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="eb0ea-133">Description</span></span>|
|---|---|
|<span data-ttu-id="eb0ea-134">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-134">**Protocol**</span></span> | <span data-ttu-id="eb0ea-135">El protocolo para filtrar la captura de paquetes.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="eb0ea-136">Los valores disponibles son TCP, UDP y All (Todos).</span><span class="sxs-lookup"><span data-stu-id="eb0ea-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="eb0ea-137">**Dirección IP local**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-137">**Local IP address**</span></span> | <span data-ttu-id="eb0ea-138">Este valor filtra la captura de paquetes a los paquetes en los que la dirección IP local coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="eb0ea-139">**Puerto local**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-139">**Local port**</span></span> | <span data-ttu-id="eb0ea-140">Este valor filtra la captura de paquetes a los paquetes en los que el puerto local coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="eb0ea-141">**Dirección IP remota**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-141">**Remote IP address**</span></span> | <span data-ttu-id="eb0ea-142">Este valor filtra la captura de paquetes a los paquetes en los que la dirección IP remota coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="eb0ea-143">**Puerto remoto**</span><span class="sxs-lookup"><span data-stu-id="eb0ea-143">**Remote port**</span></span> | <span data-ttu-id="eb0ea-144">Este valor filtra la captura de paquetes a los paquetes en los que el puerto remoto coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="eb0ea-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="eb0ea-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb0ea-145">Next steps</span></span>

<span data-ttu-id="eb0ea-146">Aprenda a administrar las capturas de paquetes a través del portal consultando [Administración de capturas de paquetes con Azure Network Watcher mediante Azure Portal](network-watcher-packet-capture-manage-portal.md) o con PowerShell consultando [Administración de capturas de paquetes con Azure Network Watcher mediante PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eb0ea-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="eb0ea-147">Aprenda a crear capturas de paquetes proactivas basadas en las alertas de máquina virtual en el artículo sobre cómo [crear una captura de paquetes desencadenada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="eb0ea-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













