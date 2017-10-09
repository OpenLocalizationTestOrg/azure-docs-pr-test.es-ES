---
title: chasis de aaaReplace en el dispositivo de la serie StorSimple 8000 | Documentos de Microsoft
description: "Describe cómo tooremove y reemplazar Hola chasis para el alojamiento principal de StorSimple o el alojamiento de EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="d62e2-103">Reemplazar el chasis de hello en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="d62e2-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="d62e2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d62e2-104">Overview</span></span>
<span data-ttu-id="d62e2-105">Este tutorial le explica cómo tooremove y reemplazar un chasis de un dispositivo de la serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="d62e2-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="d62e2-106">modelo de Hello StorSimple 8100 es un dispositivo de alojamiento (un chasis), mientras que Hola 8600 es un dispositivo de alojamiento doble (dos chasis).</span><span class="sxs-lookup"><span data-stu-id="d62e2-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="d62e2-107">Para un modelo 8600, hay potencialmente dos chasis que pudieron producirse un error en el dispositivo de hello: Hola chasis para el alojamiento principal de Hola o chasis de Hola para hello alojamiento de EBOD.</span><span class="sxs-lookup"><span data-stu-id="d62e2-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="d62e2-108">En cualquier caso, el chasis de sustitución de Hola que Microsoft envía está vacío.</span><span class="sxs-lookup"><span data-stu-id="d62e2-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="d62e2-109">No se incluirán Módulos de alimentación y refrigeración (PCM), módulos de controlador, unidades de disco de estado sólido (SSD), unidades de disco duro (HDD) o módulos EBOD.</span><span class="sxs-lookup"><span data-stu-id="d62e2-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d62e2-110">Antes de quitar y reemplazar el chasis de hello, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="d62e2-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="d62e2-111">Quitar el chasis de Hola</span><span class="sxs-lookup"><span data-stu-id="d62e2-111">Remove hello chassis</span></span>
<span data-ttu-id="d62e2-112">Realizar Hola después de chasis de pasos tooremove hello en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d62e2-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="d62e2-113">tooremove un chasis</span><span class="sxs-lookup"><span data-stu-id="d62e2-113">tooremove a chassis</span></span>
1. <span data-ttu-id="d62e2-114">Asegúrese de que ese dispositivo de StorSimple Hola está apagado y desconectado de todas las fuentes de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d62e2-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="d62e2-115">Quite todos los red hello y cables SAS, si procede.</span><span class="sxs-lookup"><span data-stu-id="d62e2-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="d62e2-116">Quitar unidad de Hola de bastidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d62e2-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="d62e2-117">Quitar cada una de las unidades de Hola y anote las ranuras de Hola desde la que se quitan.</span><span class="sxs-lookup"><span data-stu-id="d62e2-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="d62e2-118">Para obtener más información, consulte [quitar la unidad de disco de hello](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="d62e2-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="d62e2-119">En hello alojamiento de EBOD (si se trata de chasis de Hola que no se pudo), quitar los módulos de controlador EBOD Hola.</span><span class="sxs-lookup"><span data-stu-id="d62e2-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="d62e2-120">Para obtener más información, consulte [Quitar un controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="d62e2-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="d62e2-121">En hello alojamiento principal (si se trata de chasis de Hola que no se pudo), quite los controladores de Hola y tenga en cuenta las ranuras de Hola desde la que se quitan.</span><span class="sxs-lookup"><span data-stu-id="d62e2-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="d62e2-122">Para obtener más información, consulte [Quitar un controlador](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="d62e2-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="d62e2-123">Instalar el chasis de Hola</span><span class="sxs-lookup"><span data-stu-id="d62e2-123">Install hello chassis</span></span>
<span data-ttu-id="d62e2-124">Realizar Hola después de chasis de pasos tooinstall hello en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d62e2-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="d62e2-125">tooinstall un chasis</span><span class="sxs-lookup"><span data-stu-id="d62e2-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="d62e2-126">Monte el chasis de hello en bastidor Hola.</span><span class="sxs-lookup"><span data-stu-id="d62e2-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="d62e2-127">Para obtener más información, consulte [Montaje en bastidor del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montaje en bastidor del dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="d62e2-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="d62e2-128">Después de montar el chasis de hello en bastidor hello, instale los módulos de controlador de Hola Hola en que mismo coloca que estaban instaladas previamente.</span><span class="sxs-lookup"><span data-stu-id="d62e2-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="d62e2-129">Instalación Hola unidades en hello mismo posiciones y ranuras que estaban instaladas previamente en.</span><span class="sxs-lookup"><span data-stu-id="d62e2-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d62e2-130">Se recomienda que instalar SSD de hello en los espacios de hello en primer lugar y, a continuación, instalar Hola HDD.</span><span class="sxs-lookup"><span data-stu-id="d62e2-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="d62e2-131">Con Hola dispositivo montado en bastidor de Hola y Hola se instalen, conectar los orígenes de dispositivo toohello alimentación adecuadas y encienda el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d62e2-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="d62e2-132">Para obtener más información, consulte [Instalación de cables del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Instalación de cables StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="d62e2-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d62e2-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d62e2-133">Next steps</span></span>
<span data-ttu-id="d62e2-134">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="d62e2-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

