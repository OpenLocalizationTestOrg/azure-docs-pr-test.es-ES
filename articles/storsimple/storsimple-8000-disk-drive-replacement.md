---
title: una unidad de disco en un dispositivo de la serie StorSimple 8000 aaaReplace | Documentos de Microsoft
description: "Explica cómo unidad tooreplace un disco en un alojamiento principal de StorSimple o un alojamiento de EBOD."
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
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="b8eee-103">Reemplazo de una unidad de disco en un dispositivo de la serie StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="b8eee-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="b8eee-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b8eee-104">Overview</span></span>
<span data-ttu-id="b8eee-105">Este tutorial explica cómo quitar y reemplazar una unidad de disco duro que no funciona correctamente o defectuosa en un dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b8eee-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="b8eee-106">tooreplace una unidad de disco, debe:</span><span class="sxs-lookup"><span data-stu-id="b8eee-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="b8eee-107">Desactivar el bloqueo contra manipulaciones Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="b8eee-108">Quitar unidad de disco de Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-108">Remove hello disk drive</span></span>
* <span data-ttu-id="b8eee-109">Instalar la unidad de disco de reemplazo de Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8eee-110">Antes de quitar y reemplazar una unidad de disco, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b8eee-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="b8eee-111">Desactivar el bloqueo contra manipulaciones Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="b8eee-112">Este procedimiento explica cómo se pueden acoplar o desacoplar al reemplazar unidades de disco de hello bloqueos contra manipulaciones de hello en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8eee-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="b8eee-113">los bloqueos contra manipulaciones Hola se ajustan en identificadores de portadora de unidad de Hola y se tiene acceso a través de una pequeña abertura en la sección del identificador hello enganche de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="b8eee-114">Las unidades se suministran con hello bloqueos conjunto toohello bloqueado posición.</span><span class="sxs-lookup"><span data-stu-id="b8eee-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="b8eee-115">bloqueo contra manipulaciones de hello toounlock</span><span class="sxs-lookup"><span data-stu-id="b8eee-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="b8eee-116">Inserte con cuidado la llave de bloqueo de hello (un destornillador T10 "impide las alteraciones" que Microsoft proporciona) en hello abertura identificador hello y en su zócalo.</span><span class="sxs-lookup"><span data-stu-id="b8eee-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="b8eee-117">Si está activado el bloqueo contra manipulaciones de hello, indicador de hello rojo esté visible en la abertura Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Unidad de disco bloqueada](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="b8eee-119">**Figura 1** Bloqueo antisabotaje activado</span><span class="sxs-lookup"><span data-stu-id="b8eee-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="b8eee-120">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="b8eee-120">Label</span></span> | <span data-ttu-id="b8eee-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8eee-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b8eee-122">1</span><span class="sxs-lookup"><span data-stu-id="b8eee-122">1</span></span> |<span data-ttu-id="b8eee-123">Orificio indicador</span><span class="sxs-lookup"><span data-stu-id="b8eee-123">Indicator aperture</span></span> |
   | <span data-ttu-id="b8eee-124">2</span><span class="sxs-lookup"><span data-stu-id="b8eee-124">2</span></span> |<span data-ttu-id="b8eee-125">Bloqueo antisabotaje</span><span class="sxs-lookup"><span data-stu-id="b8eee-125">Antitamper lock</span></span> |
2. <span data-ttu-id="b8eee-126">Gire la llave de hello en una dirección en sentido contrario hasta que no esté visible en la abertura Hola por encima de la clave de Hola indicador rojo Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="b8eee-127">Quitar clave Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-127">Remove hello key.</span></span>
   
    ![Unidad de disco desbloqueada](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="b8eee-129">**Figura 2** Unidad de disco desbloqueada</span><span class="sxs-lookup"><span data-stu-id="b8eee-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="b8eee-130">Ahora se puede quitar la unidad de disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="b8eee-131">Siga los pasos de Hola de bloqueo de hello tooengage inversa.</span><span class="sxs-lookup"><span data-stu-id="b8eee-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="b8eee-132">Quitar unidad de disco de Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-132">Remove hello disk drive</span></span>
<span data-ttu-id="b8eee-133">El dispositivo StorSimple es compatible con una configuración de espacios de almacenamiento similares a RAID 10.</span><span class="sxs-lookup"><span data-stu-id="b8eee-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="b8eee-134">Esto implica que puede funcionar normalmente con un disco, unidad de estado sólido (SSD), o unidad de disco duro (HDD) defectuoso.</span><span class="sxs-lookup"><span data-stu-id="b8eee-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="b8eee-135">Si el sistema tiene más de un disco erróneo, no quite más de un SSD o HDD del sistema de Hola en cualquier momento en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="b8eee-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="b8eee-136">Esto puede provocar la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="b8eee-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="b8eee-137">Asegúrese de colocar un SSD de reemplazo en una ranura que previamente contenía un SSD.</span><span class="sxs-lookup"><span data-stu-id="b8eee-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="b8eee-138">Asegúrese de colocar un HDD de reemplazo en una ranura que previamente contenía un HDD.</span><span class="sxs-lookup"><span data-stu-id="b8eee-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="b8eee-139">Hola portal de Azure, las ranuras se numeran del 0 al 11.</span><span class="sxs-lookup"><span data-stu-id="b8eee-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="b8eee-140">Por lo tanto, si el portal de hello muestra que un disco en la ranura 2 ha dado error, el dispositivo de hello, busque Hola disco erróneo en la tercera ranura a contar Hola desde parte superior de hello izquierda.</span><span class="sxs-lookup"><span data-stu-id="b8eee-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="b8eee-141">Unidades de disco pueden quitar y reemplazar mientras el sistema de hello está funcionando.</span><span class="sxs-lookup"><span data-stu-id="b8eee-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="b8eee-142">tooremove una unidad</span><span class="sxs-lookup"><span data-stu-id="b8eee-142">tooremove a drive</span></span>
1. <span data-ttu-id="b8eee-143">Hola tooidentify error de disco, en hello portal de Azure, vaya tooyour dispositivo **configuración > estado del Hardware**.</span><span class="sxs-lookup"><span data-stu-id="b8eee-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="b8eee-144">Dado que puede producir un error en un disco en el alojamiento principal de Hola o en un alojamiento de EBOD (si está utilizando un modelo de 8600), mire estado de Hola de discos de hello en **componentes compartidos** y en **componentes compartidos de EBOD** .</span><span class="sxs-lookup"><span data-stu-id="b8eee-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="b8eee-145">Un disco defectuoso en cualquier gabinete se mostrará con un estado rojo.</span><span class="sxs-lookup"><span data-stu-id="b8eee-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="b8eee-146">Busque las unidades de hello en la parte delantera de Hola de alojamiento principal de Hola o alojamiento de EBOD Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="b8eee-147">Si el disco de hello no está bloqueado, continúe toohello siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="b8eee-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="b8eee-148">Si está bloqueado el disco de hello, desbloquéelo siguiendo el procedimiento de hello en [desactivar el bloqueo contra manipulaciones de hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="b8eee-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="b8eee-149">Presione Hola negro bloqueos temporales en el módulo portador de unidades de Hola y de extracción asa Hola hacia afuera desde la parte frontal de Hola de chasis de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Liberar el asa de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="b8eee-151">**Figura 3** asa de si se liberan Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="b8eee-152">Cuando el asa Hola esté completamente extendida, deslice el portador de unidades de hello fuera del chasis de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Deslizamiento del disco fuera de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="b8eee-154">**Figura 4** deslizante Hola de unidad de disco fuera de transportista Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="b8eee-155">Instalar la unidad de disco de reemplazo de Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="b8eee-156">Después de una unidad de error en el dispositivo StorSimple y haya extraído, siga este procedimiento tooreplace con una nueva unidad.</span><span class="sxs-lookup"><span data-stu-id="b8eee-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="b8eee-157">tooinsert una unidad</span><span class="sxs-lookup"><span data-stu-id="b8eee-157">tooinsert a drive</span></span>
1. <span data-ttu-id="b8eee-158">Asegúrese de asa Hola esté completamente extendida, tal como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="b8eee-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Unidad de disco con asa extendida](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="b8eee-160">**Figura 5** Unidad con asa extendida</span><span class="sxs-lookup"><span data-stu-id="b8eee-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="b8eee-161">Deslice portador de unidades de hello todos forma hello en el chasis de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Deslizamiento del disco hacia el transportador de la unidad de disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="b8eee-163">**Figura 6** deslizante portador de unidades de hello en el chasis de Hola</span><span class="sxs-lookup"><span data-stu-id="b8eee-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="b8eee-164">Con Hola Hola insertado, cierre unidad portadora asa mientras continúa portador de unidades de hello toopush en el chasis de hello, hasta que su Hola asa se cierre en una posición bloqueada.</span><span class="sxs-lookup"><span data-stu-id="b8eee-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="b8eee-165">Usar clave de bloqueo de Hola que ha proporcionado asa del portador de Microsoft (destornillador de Torx a prueba) toosecure hello en su lugar activando Hola tornillo de bloqueo un cuarto de vuelta a la derecha.</span><span class="sxs-lookup"><span data-stu-id="b8eee-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="b8eee-166">Compruebe que el reemplazo de hello fue correcto y Hola unidad está operativa.</span><span class="sxs-lookup"><span data-stu-id="b8eee-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="b8eee-167">Acceder Hola portal de Azure y navegar demasiado**configuración** > **estado del Hardware**.</span><span class="sxs-lookup"><span data-stu-id="b8eee-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="b8eee-168">En **componentes compartidos** o **componentes compartidos de EBOD**, estado de la unidad de hello debe ser verde, que indica que es correcto.</span><span class="sxs-lookup"><span data-stu-id="b8eee-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="b8eee-169">Puede tardar varias horas tooturn de estado de disco de hello verde tras la sustitución de Hola.</span><span class="sxs-lookup"><span data-stu-id="b8eee-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="b8eee-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8eee-170">Next steps</span></span>
<span data-ttu-id="b8eee-171">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b8eee-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

