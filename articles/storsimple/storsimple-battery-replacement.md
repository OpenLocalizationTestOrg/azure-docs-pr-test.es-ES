---
title: "batería de aaaReplace en el dispositivo StorSimple de Microsoft Azure | Documentos de Microsoft"
description: "Describe cómo reemplazar tooremove y mantener el módulo de batería de reserva de hello en el dispositivo StorSimple."
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
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="08408-103">Reemplazar el módulo de batería de reserva de hello en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="08408-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="08408-104">Información general</span><span class="sxs-lookup"><span data-stu-id="08408-104">Overview</span></span>
<span data-ttu-id="08408-105">alojamiento principal Hola Power y módulo de refrigeración (PCM) en el dispositivo de StorSimple de Microsoft Azure tiene un paquete de baterías adicional.</span><span class="sxs-lookup"><span data-stu-id="08408-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="08408-106">Este módulo proporciona alimentación para que hello dispositivo StorSimple puede guardar los datos si hay pérdida de alojamiento principal de toohello de alimentación de CA.</span><span class="sxs-lookup"><span data-stu-id="08408-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="08408-107">Este módulo de batería es que se hace referencia tooas hello *módulo de batería de reserva*.</span><span class="sxs-lookup"><span data-stu-id="08408-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="08408-108">módulo de batería de reserva de Hello existe únicamente para el alojamiento principal de hello en el dispositivo StorSimple (Hola alojamiento de EBOD no contiene un módulo de batería de reserva).</span><span class="sxs-lookup"><span data-stu-id="08408-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="08408-109">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="08408-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="08408-110">Quitar el módulo de batería de reserva de Hola</span><span class="sxs-lookup"><span data-stu-id="08408-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="08408-111">Instalar un nuevo módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="08408-111">Install a new backup battery module</span></span>
* <span data-ttu-id="08408-112">Mantener el módulo de batería de reserva de Hola</span><span class="sxs-lookup"><span data-stu-id="08408-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08408-113">Antes de quitar y reemplazar un módulo de baterías de reserva, revise la información de seguridad de Hola Hola [sustitución de componentes de hardware de introducción tooStorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="08408-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="08408-114">Quitar el módulo de batería de reserva de Hola</span><span class="sxs-lookup"><span data-stu-id="08408-114">Remove hello backup battery module</span></span>
<span data-ttu-id="08408-115">módulo de batería de reserva de Hello para el dispositivo StorSimple es una unidad reemplazable en campo.</span><span class="sxs-lookup"><span data-stu-id="08408-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="08408-116">Antes de instalarla en hello PCM, módulo de baterías de hello debe almacenarse en su embalaje original.</span><span class="sxs-lookup"><span data-stu-id="08408-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="08408-117">Realizar Hola después de batería de reserva de pasos tooremove Hola.</span><span class="sxs-lookup"><span data-stu-id="08408-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="08408-118">módulo de batería de reserva de hello tooremove</span><span class="sxs-lookup"><span data-stu-id="08408-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="08408-119">En el portal de Azure clásico de Hola, vaya demasiado**dispositivos** > **mantenimiento** > **estado del Hardware**.</span><span class="sxs-lookup"><span data-stu-id="08408-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="08408-120">En **componentes compartidos**, mire Hola estado de batería Hola.</span><span class="sxs-lookup"><span data-stu-id="08408-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="08408-121">Identifique el PCM de hello en qué Hola batería ha fallado.</span><span class="sxs-lookup"><span data-stu-id="08408-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="08408-122">La figura 1 muestra hello parte posterior del dispositivo de StorSimple Hola.</span><span class="sxs-lookup"><span data-stu-id="08408-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="08408-124">**Figura 1** Vista posterior del dispositivo primario que muestra los módulos PCM y del controlador</span><span class="sxs-lookup"><span data-stu-id="08408-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="08408-125">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="08408-125">Label</span></span> | <span data-ttu-id="08408-126">Descripción</span><span class="sxs-lookup"><span data-stu-id="08408-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="08408-127">1</span><span class="sxs-lookup"><span data-stu-id="08408-127">1</span></span> |<span data-ttu-id="08408-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="08408-128">PCM 0</span></span> |
   | <span data-ttu-id="08408-129">2</span><span class="sxs-lookup"><span data-stu-id="08408-129">2</span></span> |<span data-ttu-id="08408-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="08408-130">PCM 1</span></span> |
   | <span data-ttu-id="08408-131">3</span><span class="sxs-lookup"><span data-stu-id="08408-131">3</span></span> |<span data-ttu-id="08408-132">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="08408-132">Controller 0</span></span> |
   | <span data-ttu-id="08408-133">4</span><span class="sxs-lookup"><span data-stu-id="08408-133">4</span></span> |<span data-ttu-id="08408-134">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="08408-134">Controller 1</span></span> |
   
    <span data-ttu-id="08408-135">Como se muestra en el número 3 en la figura 2 hello, Hola supervisión indicador LED en PCM 0 que corresponde demasiado**error de batería** debe estar encendido.</span><span class="sxs-lookup"><span data-stu-id="08408-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane de supervisión de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="08408-137">**Figura 2** Hola de mostrando parte posterior del PCM LED indicadores de supervisión</span><span class="sxs-lookup"><span data-stu-id="08408-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="08408-138">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="08408-138">Label</span></span> | <span data-ttu-id="08408-139">Descripción</span><span class="sxs-lookup"><span data-stu-id="08408-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="08408-140">1</span><span class="sxs-lookup"><span data-stu-id="08408-140">1</span></span> |<span data-ttu-id="08408-141">Error de corriente alterna</span><span class="sxs-lookup"><span data-stu-id="08408-141">AC power failure</span></span> |
   | <span data-ttu-id="08408-142">2</span><span class="sxs-lookup"><span data-stu-id="08408-142">2</span></span> |<span data-ttu-id="08408-143">Error del ventilador</span><span class="sxs-lookup"><span data-stu-id="08408-143">Fan failure</span></span> |
   | <span data-ttu-id="08408-144">3</span><span class="sxs-lookup"><span data-stu-id="08408-144">3</span></span> |<span data-ttu-id="08408-145">Error de la batería</span><span class="sxs-lookup"><span data-stu-id="08408-145">Battery fault</span></span> |
   | <span data-ttu-id="08408-146">4</span><span class="sxs-lookup"><span data-stu-id="08408-146">4</span></span> |<span data-ttu-id="08408-147">PCM correcto</span><span class="sxs-lookup"><span data-stu-id="08408-147">PCM OK</span></span> |
   | <span data-ttu-id="08408-148">5</span><span class="sxs-lookup"><span data-stu-id="08408-148">5</span></span> |<span data-ttu-id="08408-149">Error de alimentación de CD</span><span class="sxs-lookup"><span data-stu-id="08408-149">DC power failure</span></span> |
   | <span data-ttu-id="08408-150">6</span><span class="sxs-lookup"><span data-stu-id="08408-150">6</span></span> |<span data-ttu-id="08408-151">Batería en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="08408-151">Battery healthy</span></span> |
3. <span data-ttu-id="08408-152">Hola tooremove PCM con una batería averiada, siga los pasos de hello en [quite el PCM con](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="08408-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="08408-153">Con hello PCM extraído, elevación y batería Hola girar módulo controlar hacia arriba tal como se indica en la figura siguiente de Hola y extraer la batería de hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="08408-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Quitar batería del PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="08408-155">**Figura 3** quitando batería de Hola de hello PCM</span><span class="sxs-lookup"><span data-stu-id="08408-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="08408-156">Coloque el módulo de hello en unidad reemplazable en campo Hola empaquetado.</span><span class="sxs-lookup"><span data-stu-id="08408-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="08408-157">Devolver Hola unidad defectuosa tooMicrosoft de servicio y gestión adecuados.</span><span class="sxs-lookup"><span data-stu-id="08408-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="08408-158">Instalar un nuevo módulo de baterías de reserva</span><span class="sxs-lookup"><span data-stu-id="08408-158">Install a new backup battery module</span></span>
<span data-ttu-id="08408-159">Realizar Hola después de módulo de baterías de sustitución pasos tooinstall hello en Hola PCM del alojamiento principal de hello de dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="08408-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="08408-160">módulo de baterías de hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="08408-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="08408-161">Coloque el módulo de batería de reserva de hello en la orientación correcta de Hola Hola PCM.</span><span class="sxs-lookup"><span data-stu-id="08408-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="08408-162">Presione hacia abajo el módulo de baterías de hello controlar conector de todas las Hola forma tooseat Hola.</span><span class="sxs-lookup"><span data-stu-id="08408-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="08408-163">Reemplace Hola PCM en el alojamiento principal Hola siguiendo las instrucciones de hello en [reemplazar una alimentación y refrigeración módulo en el dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="08408-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="08408-164">Una vez completada la sustitución de hello, vaya demasiado**dispositivos** > **mantenimiento** > **estado del Hardware** Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="08408-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="08408-165">Comprobar estado de Hola de hello batería toomake seguro de que Hola instalación es correcta.</span><span class="sxs-lookup"><span data-stu-id="08408-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="08408-166">Estado verde indica que la batería de hello es correcto.</span><span class="sxs-lookup"><span data-stu-id="08408-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="08408-167">Mantener el módulo de batería de reserva de Hola</span><span class="sxs-lookup"><span data-stu-id="08408-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="08408-168">En el dispositivo StorSimple, módulo de batería de reserva de hello proporciona controlador toohello de energía durante un evento de pérdida de energía.</span><span class="sxs-lookup"><span data-stu-id="08408-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="08408-169">Permite hello StorSimple dispositivo toosave datos críticos anterior tooshutting hacia abajo de una manera controlada.</span><span class="sxs-lookup"><span data-stu-id="08408-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="08408-170">Con dos baterías totalmente cargadas en hello PCM, sistema de hello puede controlar dos eventos de corte consecutivos.</span><span class="sxs-lookup"><span data-stu-id="08408-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="08408-171">Hola portal de Azure clásico, Hola **estado del Hardware** en hello **mantenimiento** página indica si está funcionando mal batería Hola o de obsolescencia de saludo se está agotando.</span><span class="sxs-lookup"><span data-stu-id="08408-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="08408-172">estado de la batería de Hola se indica mediante **batería en PCM 0** o **batería en PCM 1** en **componentes compartidos**.</span><span class="sxs-lookup"><span data-stu-id="08408-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="08408-173">Esta página muestra un estado **DEGRADADO** cuando se aproxima el final del ciclo de vida, y **ERROR** cuando se alcanza el final del ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="08408-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="08408-174">Hola batería puede mostrar **error** cuando necesita simplemente toobe cobra.</span><span class="sxs-lookup"><span data-stu-id="08408-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="08408-175">Si hello **degradado** aparece estado, se recomienda Hola siguiendo el curso de acción:</span><span class="sxs-lookup"><span data-stu-id="08408-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="08408-176">sistema de Hola que haya tenido una pérdida de energía reciente o baterías Hola pueden se está llevando a cabo mantenimiento periódico.</span><span class="sxs-lookup"><span data-stu-id="08408-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="08408-177">Observe el sistema de Hola durante 12 horas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="08408-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="08408-178">Si el estado de hello sigue siendo **degradado** después de 12 horas de alimentación de tooAC de conexión continua con hello de controladores y PCM en ejecución, a continuación, Hola batería debe toobe reemplazado.</span><span class="sxs-lookup"><span data-stu-id="08408-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="08408-179">[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) para obtener un módulo de baterías de reserva de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="08408-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="08408-180">Si se convierte en un estado de hello correcto después de 12 horas, batería Hola está operativo y solo necesita un coste de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="08408-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="08408-181">Si no ha habido un corte de alimentación de CA y Hola PCM asociado esté encendido y conectado tooAC power, batería Hola debe toobe reemplazado.</span><span class="sxs-lookup"><span data-stu-id="08408-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="08408-182">[Póngase en contacto con Microsoft Support](storsimple-contact-microsoft-support.md) tooorder un módulo de batería de reserva de reemplazo.</span><span class="sxs-lookup"><span data-stu-id="08408-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08408-183">Dispose de hello error batería según toonational y la normativa regional.</span><span class="sxs-lookup"><span data-stu-id="08408-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="08408-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08408-184">Next steps</span></span>
<span data-ttu-id="08408-185">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="08408-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

