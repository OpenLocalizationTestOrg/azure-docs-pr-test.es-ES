---
title: "Reemplazo de la batería del dispositivo Microsoft Azure StorSimple | Microsoft Docs"
description: "Describe cómo quitar, reemplazar y mantener el módulo de baterías de reserva en el dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="b6c43-103">Reemplazar el módulo de baterías de reserva en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b6c43-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="b6c43-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b6c43-104">Overview</span></span>
<span data-ttu-id="b6c43-105">El Módulo de alimentación y refrigeración (PCM) del gabinete primario en el dispositivo StorSimple de Microsoft Azure tiene un paquete de baterías adicional.</span><span class="sxs-lookup"><span data-stu-id="b6c43-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="b6c43-106">Este paquete proporciona energía para que el dispositivo StorSimple pueda guardar los datos si hay una pérdida de alimentación de CA para el gabinete principal.</span><span class="sxs-lookup"><span data-stu-id="b6c43-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="b6c43-107">Este paquete de baterías se conoce como el *módulo de baterías de reserva*.</span><span class="sxs-lookup"><span data-stu-id="b6c43-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="b6c43-108">El módulo de baterías de reserva solo existe para el gabinete principal del dispositivo StorSimple (el gabinete de EBOD no contiene un módulo de baterías de reserva).</span><span class="sxs-lookup"><span data-stu-id="b6c43-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="b6c43-109">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b6c43-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="b6c43-110">Quitar el módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="b6c43-111">Instalar un nuevo módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-111">Install a new backup battery module</span></span>
* <span data-ttu-id="b6c43-112">Mantener el módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6c43-113">Antes de quitar y reemplazar un módulo de baterías de reserva, revise la información de seguridad de [Introducción al reemplazo de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b6c43-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="b6c43-114">Quitar el módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-114">Remove the backup battery module</span></span>
<span data-ttu-id="b6c43-115">El módulo de baterías de reserva para el dispositivo StorSimple es una unidad reemplazable en situ.</span><span class="sxs-lookup"><span data-stu-id="b6c43-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="b6c43-116">Antes de instalar en el PCM, el módulo de baterías debería almacenarse en su paquete original.</span><span class="sxs-lookup"><span data-stu-id="b6c43-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="b6c43-117">Realice los siguientes pasos para extraer la batería de reserva.</span><span class="sxs-lookup"><span data-stu-id="b6c43-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="b6c43-118">Para quitar el módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="b6c43-119">En el Portal de Azure clásico, vaya a **Dispositivos** > **Mantenimiento** > **Estado de hardware**.</span><span class="sxs-lookup"><span data-stu-id="b6c43-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="b6c43-120">En **Componentes compartidos**, examine el estado de la batería.</span><span class="sxs-lookup"><span data-stu-id="b6c43-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="b6c43-121">Identifique el PCM en el que ha fallado la batería.</span><span class="sxs-lookup"><span data-stu-id="b6c43-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="b6c43-122">La Figura 1 muestra la parte posterior del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6c43-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="b6c43-124">**Figura 1** Vista posterior del dispositivo primario que muestra los módulos PCM y del controlador</span><span class="sxs-lookup"><span data-stu-id="b6c43-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="b6c43-125">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="b6c43-125">Label</span></span> | <span data-ttu-id="b6c43-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="b6c43-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b6c43-127">1</span><span class="sxs-lookup"><span data-stu-id="b6c43-127">1</span></span> |<span data-ttu-id="b6c43-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b6c43-128">PCM 0</span></span> |
   | <span data-ttu-id="b6c43-129">2</span><span class="sxs-lookup"><span data-stu-id="b6c43-129">2</span></span> |<span data-ttu-id="b6c43-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b6c43-130">PCM 1</span></span> |
   | <span data-ttu-id="b6c43-131">3</span><span class="sxs-lookup"><span data-stu-id="b6c43-131">3</span></span> |<span data-ttu-id="b6c43-132">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="b6c43-132">Controller 0</span></span> |
   | <span data-ttu-id="b6c43-133">4</span><span class="sxs-lookup"><span data-stu-id="b6c43-133">4</span></span> |<span data-ttu-id="b6c43-134">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="b6c43-134">Controller 1</span></span> |
   
    <span data-ttu-id="b6c43-135">Tal como se muestra el número 3 en la Figura 2, el LED indicador de supervisión en PCM 0 que corresponde a **Error de batería** debe estar encendido.</span><span class="sxs-lookup"><span data-stu-id="b6c43-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Backplane de supervisión de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="b6c43-137">**Figura 2** Parte posterior del PCM que muestra los LED indicadores de supervisión</span><span class="sxs-lookup"><span data-stu-id="b6c43-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="b6c43-138">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="b6c43-138">Label</span></span> | <span data-ttu-id="b6c43-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="b6c43-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b6c43-140">1</span><span class="sxs-lookup"><span data-stu-id="b6c43-140">1</span></span> |<span data-ttu-id="b6c43-141">Error de corriente alterna</span><span class="sxs-lookup"><span data-stu-id="b6c43-141">AC power failure</span></span> |
   | <span data-ttu-id="b6c43-142">2</span><span class="sxs-lookup"><span data-stu-id="b6c43-142">2</span></span> |<span data-ttu-id="b6c43-143">Error del ventilador</span><span class="sxs-lookup"><span data-stu-id="b6c43-143">Fan failure</span></span> |
   | <span data-ttu-id="b6c43-144">3</span><span class="sxs-lookup"><span data-stu-id="b6c43-144">3</span></span> |<span data-ttu-id="b6c43-145">Error de la batería</span><span class="sxs-lookup"><span data-stu-id="b6c43-145">Battery fault</span></span> |
   | <span data-ttu-id="b6c43-146">4</span><span class="sxs-lookup"><span data-stu-id="b6c43-146">4</span></span> |<span data-ttu-id="b6c43-147">PCM correcto</span><span class="sxs-lookup"><span data-stu-id="b6c43-147">PCM OK</span></span> |
   | <span data-ttu-id="b6c43-148">5</span><span class="sxs-lookup"><span data-stu-id="b6c43-148">5</span></span> |<span data-ttu-id="b6c43-149">Error de alimentación de CD</span><span class="sxs-lookup"><span data-stu-id="b6c43-149">DC power failure</span></span> |
   | <span data-ttu-id="b6c43-150">6</span><span class="sxs-lookup"><span data-stu-id="b6c43-150">6</span></span> |<span data-ttu-id="b6c43-151">Batería en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="b6c43-151">Battery healthy</span></span> |
3. <span data-ttu-id="b6c43-152">Para quitar el PCM con una batería que no funciona, siga los pasos descritos en [Quitar un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="b6c43-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="b6c43-153">Después de quitar el PCM, eleve y gire el asas del módulo de batería hacia arriba como se indica en la siguiente figura, y tire de él para quitar la batería.</span><span class="sxs-lookup"><span data-stu-id="b6c43-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Quitar batería del PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="b6c43-155">**Figura 3** Quitar la batería del PCM</span><span class="sxs-lookup"><span data-stu-id="b6c43-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="b6c43-156">Coloque el módulo en el paquete de unidad reemplazable en campo.</span><span class="sxs-lookup"><span data-stu-id="b6c43-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="b6c43-157">Devolver la unidad defectuosa a Microsoft para el mantenimiento y control adecuado.</span><span class="sxs-lookup"><span data-stu-id="b6c43-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="b6c43-158">Instalar un nuevo módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-158">Install a new backup battery module</span></span>
<span data-ttu-id="b6c43-159">Realice los pasos siguientes para instalar el módulo de baterías de sustitución en el PCM del receptáculo principal del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b6c43-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="b6c43-160">Para instalar el módulo de batería</span><span class="sxs-lookup"><span data-stu-id="b6c43-160">To install the battery module</span></span>
1. <span data-ttu-id="b6c43-161">Coloque el módulo de baterías de reserva en la orientación correcta en el PCM.</span><span class="sxs-lookup"><span data-stu-id="b6c43-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="b6c43-162">Presione el asa del módulo de batería por completo para asentar el conector.</span><span class="sxs-lookup"><span data-stu-id="b6c43-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="b6c43-163">Sustituya el PCM en el gabinete principal siguiendo las directrices de [Reemplazar un Módulo de alimentación y refrigeración en su dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b6c43-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="b6c43-164">Una vez completada la sustitución, vaya a **Dispositivos** > **Mantenimiento** >  **Estado de hardware** en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="b6c43-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="b6c43-165">Compruebe el estado de la batería para asegurarse de que la instalación fue correcta.</span><span class="sxs-lookup"><span data-stu-id="b6c43-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="b6c43-166">Un estado verde indica que el estado de la batería es correcto.</span><span class="sxs-lookup"><span data-stu-id="b6c43-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="b6c43-167">Mantener el módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="b6c43-167">Maintain the backup battery module</span></span>
<span data-ttu-id="b6c43-168">En el dispositivo StorSimple, el módulo de baterías de reserva proporciona energía al controlador durante un evento de pérdida de alimentación.</span><span class="sxs-lookup"><span data-stu-id="b6c43-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="b6c43-169">Permite que el dispositivo StorSimple guarde los datos críticos antes de apagar el equipo de una manera controlada.</span><span class="sxs-lookup"><span data-stu-id="b6c43-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="b6c43-170">Con dos baterías totalmente cargadas en los PCM, el sistema puede controlar dos eventos de pérdida consecutivos.</span><span class="sxs-lookup"><span data-stu-id="b6c43-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="b6c43-171">En el Portal de Azure clásico, el **Estado de hardware** en la página **Mantenimiento** indica si la batería funciona mal o si se aproxima el final del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="b6c43-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="b6c43-172">El estado de la batería se indica en **Batería en PCM 0** o **Batería en PCM 1** en **Componentes compartidos**.</span><span class="sxs-lookup"><span data-stu-id="b6c43-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="b6c43-173">Esta página muestra un estado **DEGRADADO** cuando se aproxima el final del ciclo de vida, y **ERROR** cuando se alcanza el final del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="b6c43-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="b6c43-174">La batería puede mostrar **ERROR** cuando simplemente necesita cargarse.</span><span class="sxs-lookup"><span data-stu-id="b6c43-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="b6c43-175">Si aparece el estado **DEGRADADO** , se recomienda lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b6c43-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="b6c43-176">Puede que el sistema haya experimentado una pérdida de energía reciente o las baterías pueden estar llevando a cabo el mantenimiento periódico.</span><span class="sxs-lookup"><span data-stu-id="b6c43-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="b6c43-177">Observe el sistema durante 12 horas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="b6c43-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="b6c43-178">Si el estado sigue siendo **DEGRADADO** después de 12 horas de conexión continua a alimentación de CA con los controladores y PCM en ejecución, a continuación, la batería debe reemplazarse.</span><span class="sxs-lookup"><span data-stu-id="b6c43-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="b6c43-179">[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para obtener un módulo de baterías de reserva de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="b6c43-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="b6c43-180">Si el estado cambia a CORRECTO después de 12 horas, la batería funciona y solo necesita una carga de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="b6c43-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="b6c43-181">Si no ha habido una pérdida de alimentación de CA asociada y el PCM está encendido y conectado a CA, debe reemplazar la batería.</span><span class="sxs-lookup"><span data-stu-id="b6c43-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="b6c43-182">[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para obtener un módulo de baterías de reserva de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="b6c43-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6c43-183">Deseche la batería que no funciona según las normas nacionales y regionales.</span><span class="sxs-lookup"><span data-stu-id="b6c43-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b6c43-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b6c43-184">Next steps</span></span>
<span data-ttu-id="b6c43-185">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b6c43-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

