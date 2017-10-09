---
title: captura de tooPacket aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de la capacidad de captura de paquetes de saludo Monitor de red"
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
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="d1cef-103">Captura de paquetes toovariable de introducción en el Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="d1cef-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="d1cef-104">Captura de paquetes de variable de Monitor de red le permite toocreate paquete captura sesiones tootrack tráfico tooand desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d1cef-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="d1cef-105">Captura de paquetes le ayuda a anomalías red toodiagnose reactivamente y proactivity.</span><span class="sxs-lookup"><span data-stu-id="d1cef-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="d1cef-106">Otros usos incluyen la recopilación de estadísticas de red, obtenga información sobre las intrusiones de red, toodebug cliente-servidor las comunicaciones y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d1cef-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="d1cef-107">La captura de paquetes es una extensión de máquina virtual que se inicia de forma remota a través de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="d1cef-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="d1cef-108">Esta capacidad facilita la carga de Hola de ejecutar manualmente una captura de paquetes en la máquina virtual de hello deseado, que permite ahorrar tiempo.</span><span class="sxs-lookup"><span data-stu-id="d1cef-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="d1cef-109">Captura de paquetes puede realizarse a través del portal de hello, PowerShell, CLI o API de REST.</span><span class="sxs-lookup"><span data-stu-id="d1cef-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="d1cef-110">Un ejemplo de cómo se puede activar la captura de paquetes es con las alertas de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d1cef-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="d1cef-111">Los filtros son proporcionados para tooensure de sesión de captura de Hola captura el tráfico que desee toomonitor.</span><span class="sxs-lookup"><span data-stu-id="d1cef-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="d1cef-112">Los filtros se basan en la información de 5-tupla (protocolo, dirección IP local, dirección IP remota, el puerto local y puerto remoto).</span><span class="sxs-lookup"><span data-stu-id="d1cef-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="d1cef-113">Hola capturan datos se almacenan en el disco local de Hola o un blob de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d1cef-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="d1cef-114">Hay un límite de 10 sesiones de captura de paquetes por región y suscripción.</span><span class="sxs-lookup"><span data-stu-id="d1cef-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="d1cef-115">Este límite aplica solo a las sesiones de toohello y no hay ningún toohello archivos de captura de paquetes de guardados localmente en hello VM o en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d1cef-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1cef-116">La captura de paquetes requiere una extensión de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="d1cef-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="d1cef-117">Para instalar la extensión de hello en una máquina virtual de Windows, visite [extensión de máquina virtual de agente de Monitor de red de Azure para Windows](../virtual-machines/windows/extensions-nwa.md) y para la visita de VM de Linux [extensión de máquina virtual de agente de Monitor de red de Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="d1cef-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="d1cef-118">información de hello tooreduce capturar información de hello tooonly que desee, Hola siguientes opciones está disponible para una sesión de captura de paquetes:</span><span class="sxs-lookup"><span data-stu-id="d1cef-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="d1cef-119">**Configuración de captura**</span><span class="sxs-lookup"><span data-stu-id="d1cef-119">**Capture configuration**</span></span>

|<span data-ttu-id="d1cef-120">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d1cef-120">Property</span></span>|<span data-ttu-id="d1cef-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1cef-121">Description</span></span>|
|---|---|
|<span data-ttu-id="d1cef-122">**Número máximo de bytes por paquete (bytes)**</span><span class="sxs-lookup"><span data-stu-id="d1cef-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="d1cef-123">Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco.</span><span class="sxs-lookup"><span data-stu-id="d1cef-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="d1cef-124">Hola número de bytes de cada paquete que se capturan, se capturan todos los bytes si se deja en blanco.</span><span class="sxs-lookup"><span data-stu-id="d1cef-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="d1cef-125">Si tiene un solo encabezado de IPv4 de hello: indicar 34 aquí</span><span class="sxs-lookup"><span data-stu-id="d1cef-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="d1cef-126">**Número máximo de bytes por sesión (bytes)**</span><span class="sxs-lookup"><span data-stu-id="d1cef-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="d1cef-127">Número total de bytes en la se captura, una vez que se alcanza el valor de Hola Hola finaliza la sesión.</span><span class="sxs-lookup"><span data-stu-id="d1cef-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="d1cef-128">**Límite de tiempo (segundos)**</span><span class="sxs-lookup"><span data-stu-id="d1cef-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="d1cef-129">Establece una restricción horaria en el paquete de saludo capturar sesión.</span><span class="sxs-lookup"><span data-stu-id="d1cef-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="d1cef-130">valor predeterminado de Hello es 18000 segundos o 5 horas.</span><span class="sxs-lookup"><span data-stu-id="d1cef-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="d1cef-131">**Filtrado (opcional)**</span><span class="sxs-lookup"><span data-stu-id="d1cef-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="d1cef-132">Propiedad</span><span class="sxs-lookup"><span data-stu-id="d1cef-132">Property</span></span>|<span data-ttu-id="d1cef-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1cef-133">Description</span></span>|
|---|---|
|<span data-ttu-id="d1cef-134">**Protocolo**</span><span class="sxs-lookup"><span data-stu-id="d1cef-134">**Protocol**</span></span> | <span data-ttu-id="d1cef-135">captura de Hello toofilter de protocolo para el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="d1cef-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="d1cef-136">los valores disponibles de Hello son TCP, UDP y todos.</span><span class="sxs-lookup"><span data-stu-id="d1cef-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="d1cef-137">**Dirección IP local**</span><span class="sxs-lookup"><span data-stu-id="d1cef-137">**Local IP address**</span></span> | <span data-ttu-id="d1cef-138">Este valor filtra toopackets de captura de paquetes de saludo donde la dirección IP local Hola coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d1cef-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="d1cef-139">**Puerto local**</span><span class="sxs-lookup"><span data-stu-id="d1cef-139">**Local port**</span></span> | <span data-ttu-id="d1cef-140">Este paquete de saludo de filtros de valor capturar toopackets donde puerto local Hola coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d1cef-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="d1cef-141">**Dirección IP remota**</span><span class="sxs-lookup"><span data-stu-id="d1cef-141">**Remote IP address**</span></span> | <span data-ttu-id="d1cef-142">Este paquete de saludo de filtros de valor capturar toopackets donde hello remoto IP coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d1cef-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="d1cef-143">**Puerto remoto**</span><span class="sxs-lookup"><span data-stu-id="d1cef-143">**Remote port**</span></span> | <span data-ttu-id="d1cef-144">Este paquete de saludo de filtros de valor capturar toopackets donde puerto remoto hello coincide con este valor de filtro.</span><span class="sxs-lookup"><span data-stu-id="d1cef-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="d1cef-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1cef-145">Next steps</span></span>

<span data-ttu-id="d1cef-146">Obtenga información acerca de cómo administrar las capturas de paquetes a través del portal de hello visitando [administrar captura de paquetes en el portal de Azure hello](network-watcher-packet-capture-manage-portal.md) o con PowerShell visitando [administrar paquetes de captura con PowerShell](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d1cef-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="d1cef-147">Obtenga información acerca de cómo se captura toocreate automático paquetes basados en alertas de máquina virtual visitando [crear una captura de paquetes desencadenadas alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="d1cef-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













