---
title: Reemplazo de un disco duro en un dispositivo StorSimple | Microsoft Docs
description: "Explica cómo reemplazar una unidad de disco en un receptáculo principal de StorSimple o un receptáculo EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 0659ab9d304dbfcce72e8c3c79edad68e70b9630
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="bfd3a-103">Reemplazar un disco duro en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="bfd3a-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="bfd3a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="bfd3a-104">Overview</span></span>
<span data-ttu-id="bfd3a-105">Este tutorial explica cómo quitar y reemplazar una unidad de disco duro que no funciona correctamente o defectuosa en un dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="bfd3a-106">Para reemplazar una unidad de disco, necesitará:</span><span class="sxs-lookup"><span data-stu-id="bfd3a-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="bfd3a-107">Desactivar el bloqueo antisabotaje</span><span class="sxs-lookup"><span data-stu-id="bfd3a-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="bfd3a-108">Quitar la unidad de disco</span><span class="sxs-lookup"><span data-stu-id="bfd3a-108">Remove the disk drive</span></span>
* <span data-ttu-id="bfd3a-109">Instalar la unidad de disco de reemplazo</span><span class="sxs-lookup"><span data-stu-id="bfd3a-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bfd3a-110">Antes de quitar y reemplazar una unidad de disco, revise la información de seguridad en [Reemplazo de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="bfd3a-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="bfd3a-111">Desactivar el bloqueo antisabotaje</span><span class="sxs-lookup"><span data-stu-id="bfd3a-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="bfd3a-112">Este procedimiento explica cómo pueden activarse o desactivarse los bloqueos antisabotaje del dispositivo StorSimple al reemplazar las unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="bfd3a-113">Los bloqueos antisabotaje se instalan en las asas transportadoras de la unidad, y se accede a ellos a través de un pequeño orificio en la sección del pestillo del asa.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="bfd3a-114">Las unidades se suministran con los bloqueos establecidos en la posición bloqueada.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="bfd3a-115">Para desbloquear el bloqueo antisabotaje</span><span class="sxs-lookup"><span data-stu-id="bfd3a-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="bfd3a-116">Inserte cuidadosamente la clave de bloqueo (un destornillador T10 "inviolable" proporcionado por Microsoft) en el orificio del asa y en la toma.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="bfd3a-117">Si el bloqueo antisabotaje está activado, el indicador rojo está visible en el orificio.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
   > 
   > 
   
    ![Unidad de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="bfd3a-119">**Figura 1** Bloqueo antisabotaje activado</span><span class="sxs-lookup"><span data-stu-id="bfd3a-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="bfd3a-120">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="bfd3a-120">Label</span></span> | <span data-ttu-id="bfd3a-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="bfd3a-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="bfd3a-122">1</span><span class="sxs-lookup"><span data-stu-id="bfd3a-122">1</span></span> |<span data-ttu-id="bfd3a-123">Orificio indicador</span><span class="sxs-lookup"><span data-stu-id="bfd3a-123">Indicator aperture</span></span> |
   | <span data-ttu-id="bfd3a-124">2</span><span class="sxs-lookup"><span data-stu-id="bfd3a-124">2</span></span> |<span data-ttu-id="bfd3a-125">Bloqueo antisabotaje</span><span class="sxs-lookup"><span data-stu-id="bfd3a-125">Antitamper lock</span></span> |
2. <span data-ttu-id="bfd3a-126">Gire la clave hacia la derecha hasta que el indicador rojo no esté visible en el orificio por encima de la clave.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="bfd3a-127">Quite la llave.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-127">Remove the key.</span></span>
   
    ![Unidad de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="bfd3a-129">**Figura 2** Unidad de disco desbloqueada</span><span class="sxs-lookup"><span data-stu-id="bfd3a-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="bfd3a-130">Ahora se puede quitar la unidad de disco.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="bfd3a-131">Siga los pasos en orden inverso para activar el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="bfd3a-132">Quitar la unidad de disco</span><span class="sxs-lookup"><span data-stu-id="bfd3a-132">Remove the disk drive</span></span>
<span data-ttu-id="bfd3a-133">El dispositivo StorSimple es compatible con una configuración de espacios de almacenamiento similares a RAID 10.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="bfd3a-134">Esto implica que puede funcionar normalmente con un disco, unidad de estado sólido (SSD), o unidad de disco duro (HDD) defectuoso.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="bfd3a-135">Si el sistema tiene más de un disco defectuoso, no quite más de un SSD o unidad de disco duro del sistema en un determinado momento.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="bfd3a-136">Esto puede provocar la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="bfd3a-137">Asegúrese de colocar un SSD de reemplazo en una ranura que previamente contenía un SSD.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="bfd3a-138">Asegúrese de colocar un HDD de reemplazo en una ranura que previamente contenía un HDD.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="bfd3a-139">En el Portal de Azure clásico, las ranuras se numeran de 0 a 11.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-139">In the Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="bfd3a-140">Por lo tanto, si el portal muestra que ha fallado un disco en la ranura 2, en el dispositivo, busque el disco defectuoso en la tercera ranura de la parte superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="bfd3a-141">Las unidades de disco se pueden quitar y reemplazar mientras el sistema está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="bfd3a-142">Para quitar una unidad</span><span class="sxs-lookup"><span data-stu-id="bfd3a-142">To remove a drive</span></span>
1. <span data-ttu-id="bfd3a-143">Para identificar el disco con errores, en el Portal de Azure clásico, vaya a **Dispositivos** > **Mantenimiento** > **Estado de hardware**.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-143">To identify the failed disk, in the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="bfd3a-144">Dado que se puede producir un error en un disco en el gabinete principal o en el gabinete EBOD (si utiliza un modelo 8600), examine el estado de los discos en **Componentes compartidos** y en **Componentes compartidos del receptáculo EBOD**.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="bfd3a-145">Un disco defectuoso en cualquier gabinete se mostrará con un estado rojo.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="bfd3a-146">Busque las unidades en la parte frontal del gabinete principal o del gabinete EBOD.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="bfd3a-147">Si el disco está desbloqueado, continúe con el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="bfd3a-148">Si el disco está bloqueado, desbloquéelo siguiendo el procedimiento descrito en [Desactivar el bloqueo antisabotaje](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="bfd3a-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="bfd3a-149">Presione el pestillo negro en el módulo transportador de unidades y tire del asa transportadora de la unidad hacia afuera y lejos de la parte frontal del chasis.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span> 
   
    ![Liberar el asa de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="bfd3a-151">**Figura 3** Liberar el asa de la unidad</span><span class="sxs-lookup"><span data-stu-id="bfd3a-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="bfd3a-152">Cuando el asa transportadora de la unidad está totalmente extendida, deslice el transportador de la unidad fuera del chasis.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Deslizamiento del disco fuera de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="bfd3a-154">**Figura 4** Deslizamiento de la unidad de disco fuera del transportador</span><span class="sxs-lookup"><span data-stu-id="bfd3a-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="bfd3a-155">Instalar la unidad de disco de reemplazo</span><span class="sxs-lookup"><span data-stu-id="bfd3a-155">Install the replacement disk drive</span></span>
<span data-ttu-id="bfd3a-156">Después de que se ha producido un error en la unidad de su dispositivo StorSimple y de que la haya quitado, siga este procedimiento para reemplazarla por una nueva unidad.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="bfd3a-157">Para insertar una unidad</span><span class="sxs-lookup"><span data-stu-id="bfd3a-157">To insert a drive</span></span>
1. <span data-ttu-id="bfd3a-158">Asegúrese de que el asa transportadora de la unidad esté totalmente extendida, como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Unidad de disco con asa extendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="bfd3a-160">**Figura 5** Unidad con asa extendida</span><span class="sxs-lookup"><span data-stu-id="bfd3a-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="bfd3a-161">Deslice el transportador de la unidad por completo hacia el chasis.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-161">Slide the drive carrier all the way into the chassis.</span></span> 
   
    ![Deslizamiento del disco hacia el transportador de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="bfd3a-163">**Figura 6** Deslizamiento del transportador de la unidad hacia el chasis</span><span class="sxs-lookup"><span data-stu-id="bfd3a-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="bfd3a-164">Con el transportador de la unidad insertado, cierre el asa transportadora de la unidad mientras continúa empujando el transportador de la unidad hacia el chasis, hasta que el asa transportadora de la unidad encaje en una posición de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="bfd3a-165">Utilice la llave de bloqueo proporcionada por Microsoft (destornillador Torx inviolable) para fijar el asa transportadora en su lugar girando el destornillador de bloqueo un cuarto de vuelta hacia la derecha.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="bfd3a-166">Compruebe que el reemplazo se realizó correctamente y que la unidad funcione. Para ello, acceda al Portal de Azure clásico y vaya a **Mantenimiento** > **Estado de hardware**.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-166">Verify that the replacement was successful and the drive is operational by accessing the Azure classic portal and navigating to **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="bfd3a-167">En **Componentes compartidos** o **Componentes compartidos del receptáculo EBOD**, el estado de la unidad debe ser verde, lo que indica que está en buenas condiciones.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-167">Under **Shared Components** or **EBOD enclosure Shared Components**, the drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bfd3a-168">Puede tardar varias horas para que el estado del disco cambie a verde, después de la sustitución.</span><span class="sxs-lookup"><span data-stu-id="bfd3a-168">It may take several hours for the disk status to turn green after the replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="bfd3a-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfd3a-169">Next steps</span></span>
<span data-ttu-id="bfd3a-170">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="bfd3a-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

