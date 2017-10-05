---
title: Reemplazo del chasis del dispositivo de la serie 8000 de StorSimple | Microsoft Docs
description: "Describe cómo quitar y reemplazar el chasis del gabinete EBOD y del gabinete principal de StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 073fcf0064f1d1482f4683d733f00cf918ff2f38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a><span data-ttu-id="1d534-103">Reemplazar el chasis en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="1d534-103">Replace the chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="1d534-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1d534-104">Overview</span></span>
<span data-ttu-id="1d534-105">Este tutorial explica cómo quitar y reemplazar un chasis en un dispositivo de la serie 8000 de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d534-105">This tutorial explains how to remove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="1d534-106">El modelo StorSimple 8100 es un dispositivo de un solo gabinete (un chasis), mientras que el 8600 es un dispositivo de dos gabinetes (dos chasis).</span><span class="sxs-lookup"><span data-stu-id="1d534-106">The StorSimple 8100 model is a single enclosure device (one chassis), whereas the 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="1d534-107">Para un modelo 8600, hay potencialmente dos chasis que pueden producir un error en el dispositivo: el chasis para el gabinete principal o el chasis del gabinete EBOD.</span><span class="sxs-lookup"><span data-stu-id="1d534-107">For an 8600 model, there are potentially two chassis that could fail in the device: the chassis for the primary enclosure or the chassis for the EBOD enclosure.</span></span>

<span data-ttu-id="1d534-108">En cualquier caso, el chasis de reemplazo que se distribuye por Microsoft está vacío.</span><span class="sxs-lookup"><span data-stu-id="1d534-108">In either case, the replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="1d534-109">No se incluirán Módulos de alimentación y refrigeración (PCM), módulos de controlador, unidades de disco de estado sólido (SSD), unidades de disco duro (HDD) o módulos EBOD.</span><span class="sxs-lookup"><span data-stu-id="1d534-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d534-110">Antes de quitar y reemplazar el chasis, revise la información de seguridad en [Reemplazo de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1d534-110">Before removing and replacing the chassis, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-the-chassis"></a><span data-ttu-id="1d534-111">Quitar el chasis</span><span class="sxs-lookup"><span data-stu-id="1d534-111">Remove the chassis</span></span>
<span data-ttu-id="1d534-112">Realice los pasos siguientes para quitar el chasis en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d534-112">Perform the following steps to remove the chassis on your StorSimple device.</span></span>

#### <a name="to-remove-a-chassis"></a><span data-ttu-id="1d534-113">Para quitar un chasis</span><span class="sxs-lookup"><span data-stu-id="1d534-113">To remove a chassis</span></span>
1. <span data-ttu-id="1d534-114">Asegúrese de que el dispositivo StorSimple esté apagado y desconectado de todas las fuentes de alimentación.</span><span class="sxs-lookup"><span data-stu-id="1d534-114">Make sure that the StorSimple device is shut down and disconnected from all the power sources.</span></span>
2. <span data-ttu-id="1d534-115">Quite todos los cables de red y SAS, si corresponde.</span><span class="sxs-lookup"><span data-stu-id="1d534-115">Remove all the network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="1d534-116">Quite la unidad del bastidor.</span><span class="sxs-lookup"><span data-stu-id="1d534-116">Remove the unit from the rack.</span></span>
4. <span data-ttu-id="1d534-117">Quite cada una de las unidades de disco y tenga en cuenta las ranuras de las que se quitan.</span><span class="sxs-lookup"><span data-stu-id="1d534-117">Remove each of the drives and note the slots from which they are removed.</span></span> <span data-ttu-id="1d534-118">Para obtener más información, consulte [Quitar la unidad de disco](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="1d534-118">For more information, see [Remove the disk drive](storsimple-8000-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="1d534-119">En el gabinete EBOD (si es el chasis que produjo un error), quite los módulos del controlador EBOD.</span><span class="sxs-lookup"><span data-stu-id="1d534-119">On the EBOD enclosure (if this is the chassis that failed), remove the EBOD controller modules.</span></span> <span data-ttu-id="1d534-120">Para obtener más información, consulte [Quitar un controlador EBOD](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="1d534-120">For more information, see [Remove an EBOD controller](storsimple-8000-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span>
   
    <span data-ttu-id="1d534-121">En el gabinete principal (si es el chasis que produjo un error), quite los controladores y tenga en cuenta las ranuras de las que se quitaron.</span><span class="sxs-lookup"><span data-stu-id="1d534-121">On the primary enclosure (if this is the chassis that failed), remove the controllers and note the slots from which they are removed.</span></span> <span data-ttu-id="1d534-122">Para obtener más información, consulte [Quitar un controlador](storsimple-8000-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="1d534-122">For more information, see [Remove a controller](storsimple-8000-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-the-chassis"></a><span data-ttu-id="1d534-123">Instalar el chasis</span><span class="sxs-lookup"><span data-stu-id="1d534-123">Install the chassis</span></span>
<span data-ttu-id="1d534-124">Realice los pasos siguientes para instalar el chasis en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d534-124">Perform the following steps to install the chassis on your StorSimple device.</span></span>

#### <a name="to-install-a-chassis"></a><span data-ttu-id="1d534-125">Para instalar un chasis</span><span class="sxs-lookup"><span data-stu-id="1d534-125">To install a chassis</span></span>
1. <span data-ttu-id="1d534-126">Monte el chasis en el bastidor.</span><span class="sxs-lookup"><span data-stu-id="1d534-126">Mount the chassis in the rack.</span></span> <span data-ttu-id="1d534-127">Para obtener más información, consulte [Montaje en bastidor del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) o [Montaje en bastidor del dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="1d534-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="1d534-128">Después de que el chasis está montado en el bastidor, instale los módulos de controlador en las mismas posiciones en las que estaban previamente instaladas.</span><span class="sxs-lookup"><span data-stu-id="1d534-128">After the chassis is mounted in the rack, install the controller modules in the same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="1d534-129">Instale las unidades en las mismas posiciones y ranuras en las que estaban previamente instaladas.</span><span class="sxs-lookup"><span data-stu-id="1d534-129">Install the drives in the same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d534-130">Se recomienda que primero instale las SSD en las ranuras y, luego, instale los discos duros.</span><span class="sxs-lookup"><span data-stu-id="1d534-130">We recommend that you install the SSDs in the slots first, and then install the HDDs.</span></span>
  
4. <span data-ttu-id="1d534-131">Con el dispositivo montado en el bastidor y los componentes instalados, conecte el dispositivo a las fuentes de alimentación adecuadas y encienda el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1d534-131">With the device mounted in the rack and the components installed, connect your device to the appropriate power sources, and turn on the device.</span></span> <span data-ttu-id="1d534-132">Para obtener más información, consulte [Instalación de cables del dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [Instalación de cables StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="1d534-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d534-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1d534-133">Next steps</span></span>
<span data-ttu-id="1d534-134">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1d534-134">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

