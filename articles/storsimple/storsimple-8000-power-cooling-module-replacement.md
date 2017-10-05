---
title: Reemplazar un PCM en el dispositivo de la serie StorSimple 8000 | Microsoft Docs
description: "Explica cómo quitar y reemplazar el Módulo de alimentación y refrigeración (PCM) en el dispositivo StorSimple"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 7d181e6e434c998573dbea4b541cfacf7a28ee66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="9caf9-103">Reemplazar un Módulo de alimentación y de refrigeración en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="9caf9-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="9caf9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9caf9-104">Overview</span></span>
<span data-ttu-id="9caf9-105">El Módulo de alimentación y refrigeración (PCM) en el dispositivo StorSimple de Microsoft Azure consta de una fuente de alimentación y ventiladores que se controlan a través de los gabinetes EBOD y principal.</span><span class="sxs-lookup"><span data-stu-id="9caf9-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="9caf9-106">Hay un único modelo de PCM que está certificado para cada gabinete.</span><span class="sxs-lookup"><span data-stu-id="9caf9-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="9caf9-107">El gabinete principal está certificado para un PCM de 764 W y el gabinete EBOD está certificado para un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="9caf9-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="9caf9-108">Aunque los PCM para el gabinete principal y el gabinete EBOD son diferentes, el procedimiento de reemplazo es idéntico.</span><span class="sxs-lookup"><span data-stu-id="9caf9-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="9caf9-109">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9caf9-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="9caf9-110">Quitar un PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-110">Remove a PCM</span></span>
* <span data-ttu-id="9caf9-111">Instalar un PCM de reemplazo</span><span class="sxs-lookup"><span data-stu-id="9caf9-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9caf9-112">Antes de quitar y reemplazar un PCM, revise la información de seguridad en [Reemplazo de componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9caf9-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="9caf9-113">Antes de reemplazar un PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-113">Before you replace a PCM</span></span>
<span data-ttu-id="9caf9-114">Tenga en cuenta los siguientes aspectos importantes antes de reemplazar el PCM:</span><span class="sxs-lookup"><span data-stu-id="9caf9-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="9caf9-115">Si se produce un error en la fuente de alimentación del PCM, deje instalado el módulo defectuoso, pero quite el cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="9caf9-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="9caf9-116">El ventilador continuará recibiendo  alimentación del gabinete y continuará proporcionando la refrigeración adecuada.</span><span class="sxs-lookup"><span data-stu-id="9caf9-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="9caf9-117">Si se produce un error en el ventilador, el PCM debe reemplazarse inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="9caf9-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="9caf9-118">Antes de quitar el PCM, desconecte la alimentación de PCM desactivando el conmutador principal (si existe) o quitando físicamente el cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="9caf9-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="9caf9-119">Esto proporciona una advertencia al sistema sobre un inminente corte de energía.</span><span class="sxs-lookup"><span data-stu-id="9caf9-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="9caf9-120">Asegúrese de que el otro PCM funciona para la operación continua del sistema antes de reemplazar el PCM defectuoso.</span><span class="sxs-lookup"><span data-stu-id="9caf9-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="9caf9-121">Tan pronto como sea posible, un PCM defectuoso debe sustituirse por un PCM totalmente operativo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="9caf9-122">El reemplazo del módulo del PCM tarda solo algunos minutos en completarse, pero se debe completar en los 10 minutos posteriores a haber quitado el PCM defectuoso para evitar el sobrecalentamiento.</span><span class="sxs-lookup"><span data-stu-id="9caf9-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="9caf9-123">Tenga en cuenta que los módulos de reemplazo PCM de 764 W que se envían desde fábrica no contienen el módulo de batería de reserva.</span><span class="sxs-lookup"><span data-stu-id="9caf9-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="9caf9-124">Tendrá que extraer la batería del PCM defectuoso e insertarla en el módulo de reemplazo antes de realizar el reemplazo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="9caf9-125">Para obtener más información, consulte cómo [extraer e insertar un módulo de batería de reserva](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9caf9-125">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="9caf9-126">Quitar un PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-126">Remove a PCM</span></span>
<span data-ttu-id="9caf9-127">Siga estas instrucciones cuando esté preparado para quitar un Módulo de alimentación y refrigeración (PCM) de su dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9caf9-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="9caf9-128">Antes de quitar el PCM, compruebe que tiene un reemplazo correcto (764 W para el gabinete principal) o 580 W para el gabinete EBOD.</span><span class="sxs-lookup"><span data-stu-id="9caf9-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="9caf9-129">Para quitar un PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-129">To remove a PCM</span></span>
1. <span data-ttu-id="9caf9-130">En el Portal de Azure clásico, haga clic en **Configuración > Supervisar > Estado del hardware**.</span><span class="sxs-lookup"><span data-stu-id="9caf9-130">In the Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="9caf9-131">Compruebe el estado de los componentes de PCM en **Componentes compartidos** para identificar qué PCM ha generado el error:</span><span class="sxs-lookup"><span data-stu-id="9caf9-131">Check the status of the PCM components under **Shared components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="9caf9-132">Si una fuente de alimentación en PCM 0 está defectuosa, el estado de **Fuente de alimentación en PCM 0** será rojo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="9caf9-133">Si una fuente de alimentación en PCM 1 está defectuosa, el estado de **Fuente de alimentación en PCM 1** será rojo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="9caf9-134">Si ha fallado el ventilador de PCM 1, el estado de **Refrigeración 0 para PCM 0** o **Refrigeración 1 para PCM 0** será rojo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="9caf9-135">Busque el PCM defectuoso en la parte posterior del gabinete principal.</span><span class="sxs-lookup"><span data-stu-id="9caf9-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="9caf9-136">Si está ejecutando un modelo 8600, identifique el gabinete principal examinando el número de identificación de unidad de sistema que se muestra en el pantalla LED del panel frontal.</span><span class="sxs-lookup"><span data-stu-id="9caf9-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="9caf9-137">El identificador de unidad predeterminado que se muestra en el gabinete principal es **00**, mientras que el de la unidad predeterminada en el receptáculo EBOD es **01**.</span><span class="sxs-lookup"><span data-stu-id="9caf9-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="9caf9-138">El diagrama y la tabla siguiente explican el panel frontal de la pantalla LED.</span><span class="sxs-lookup"><span data-stu-id="9caf9-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![Identificador del sistema en el panel frontal OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="9caf9-140">**Figura 1** Panel frontal del dispositivo</span><span class="sxs-lookup"><span data-stu-id="9caf9-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="9caf9-141">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="9caf9-141">Label</span></span> | <span data-ttu-id="9caf9-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="9caf9-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="9caf9-143">1</span><span class="sxs-lookup"><span data-stu-id="9caf9-143">1</span></span> |<span data-ttu-id="9caf9-144">Botón Silencio</span><span class="sxs-lookup"><span data-stu-id="9caf9-144">Mute button</span></span> |
   | <span data-ttu-id="9caf9-145">2</span><span class="sxs-lookup"><span data-stu-id="9caf9-145">2</span></span> |<span data-ttu-id="9caf9-146">Alimentación del sistema</span><span class="sxs-lookup"><span data-stu-id="9caf9-146">System power</span></span> |
   | <span data-ttu-id="9caf9-147">3</span><span class="sxs-lookup"><span data-stu-id="9caf9-147">3</span></span> |<span data-ttu-id="9caf9-148">Error de módulo</span><span class="sxs-lookup"><span data-stu-id="9caf9-148">Module fault</span></span> |
   | <span data-ttu-id="9caf9-149">4</span><span class="sxs-lookup"><span data-stu-id="9caf9-149">4</span></span> |<span data-ttu-id="9caf9-150">Error lógico</span><span class="sxs-lookup"><span data-stu-id="9caf9-150">Logical fault</span></span> |
   | <span data-ttu-id="9caf9-151">5</span><span class="sxs-lookup"><span data-stu-id="9caf9-151">5</span></span> |<span data-ttu-id="9caf9-152">Pantalla de identificación de la unidad</span><span class="sxs-lookup"><span data-stu-id="9caf9-152">Unit ID display</span></span> |
3. <span data-ttu-id="9caf9-153">Los LED indicadores de supervisión en la parte posterior del gabinete principal también pueden utilizarse para identificar el PCM defectuoso.</span><span class="sxs-lookup"><span data-stu-id="9caf9-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="9caf9-154">Vea la siguiente tabla y diagrama para aprender a usar los LED para localizar el PCM defectuoso.</span><span class="sxs-lookup"><span data-stu-id="9caf9-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="9caf9-155">Por ejemplo, si el LED correspondiente a **Error del ventilador** está encendido, el ventilador ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="9caf9-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="9caf9-156">Del mismo modo, si el LED correspondiente a **Error de CA** está encendido, el sistema de alimentación ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="9caf9-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Backplane de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="9caf9-158">**Figura 2** Parte posterior del PCM con LED indicadores</span><span class="sxs-lookup"><span data-stu-id="9caf9-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="9caf9-159">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="9caf9-159">Label</span></span> | <span data-ttu-id="9caf9-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="9caf9-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="9caf9-161">1</span><span class="sxs-lookup"><span data-stu-id="9caf9-161">1</span></span> |<span data-ttu-id="9caf9-162">Error de corriente alterna</span><span class="sxs-lookup"><span data-stu-id="9caf9-162">AC power failure</span></span> |
   | <span data-ttu-id="9caf9-163">2</span><span class="sxs-lookup"><span data-stu-id="9caf9-163">2</span></span> |<span data-ttu-id="9caf9-164">Error del ventilador</span><span class="sxs-lookup"><span data-stu-id="9caf9-164">Fan failure</span></span> |
   | <span data-ttu-id="9caf9-165">3</span><span class="sxs-lookup"><span data-stu-id="9caf9-165">3</span></span> |<span data-ttu-id="9caf9-166">Error de la batería</span><span class="sxs-lookup"><span data-stu-id="9caf9-166">Battery fault</span></span> |
   | <span data-ttu-id="9caf9-167">4</span><span class="sxs-lookup"><span data-stu-id="9caf9-167">4</span></span> |<span data-ttu-id="9caf9-168">PCM correcto</span><span class="sxs-lookup"><span data-stu-id="9caf9-168">PCM OK</span></span> |
   | <span data-ttu-id="9caf9-169">5</span><span class="sxs-lookup"><span data-stu-id="9caf9-169">5</span></span> |<span data-ttu-id="9caf9-170">Error de alimentación de CD</span><span class="sxs-lookup"><span data-stu-id="9caf9-170">DC power failure</span></span> |
   | <span data-ttu-id="9caf9-171">6</span><span class="sxs-lookup"><span data-stu-id="9caf9-171">6</span></span> |<span data-ttu-id="9caf9-172">Batería en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="9caf9-172">Battery healthy</span></span> |
4. <span data-ttu-id="9caf9-173">Consulte el siguiente diagrama de la parte posterior del dispositivo StorSimple para encontrar el módulo PCM defectuoso.</span><span class="sxs-lookup"><span data-stu-id="9caf9-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="9caf9-174">PCM 0 está a la izquierda y PCM 1 está a la derecha.</span><span class="sxs-lookup"><span data-stu-id="9caf9-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="9caf9-175">La tabla siguiente explica los módulos.</span><span class="sxs-lookup"><span data-stu-id="9caf9-175">The table that follows explains the modules.</span></span>
   
     ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="9caf9-177">**Figura 3** Parte posterior de dispositivo con módulos de complementos</span><span class="sxs-lookup"><span data-stu-id="9caf9-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="9caf9-178">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="9caf9-178">Label</span></span> | <span data-ttu-id="9caf9-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="9caf9-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="9caf9-180">1</span><span class="sxs-lookup"><span data-stu-id="9caf9-180">1</span></span> |<span data-ttu-id="9caf9-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="9caf9-181">PCM 0</span></span> |
   | <span data-ttu-id="9caf9-182">2</span><span class="sxs-lookup"><span data-stu-id="9caf9-182">2</span></span> |<span data-ttu-id="9caf9-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="9caf9-183">PCM 1</span></span> |
   | <span data-ttu-id="9caf9-184">3</span><span class="sxs-lookup"><span data-stu-id="9caf9-184">3</span></span> |<span data-ttu-id="9caf9-185">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="9caf9-185">Controller 0</span></span> |
   | <span data-ttu-id="9caf9-186">4</span><span class="sxs-lookup"><span data-stu-id="9caf9-186">4</span></span> |<span data-ttu-id="9caf9-187">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="9caf9-187">Controller 1</span></span> |
5. <span data-ttu-id="9caf9-188">Desactive el PCM defectuoso y desconecte el cable de la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="9caf9-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="9caf9-189">Ahora puede quitar el PCM.</span><span class="sxs-lookup"><span data-stu-id="9caf9-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="9caf9-190">Sujete el pestillo y el costado del asa del PCM entre el pulgar y el índice, y apriételos para abrir el asa.</span><span class="sxs-lookup"><span data-stu-id="9caf9-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Abrir el asa del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="9caf9-192">**Figura 4** Abrir el asa del PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="9caf9-193">Sujete el asa y quite el PCM.</span><span class="sxs-lookup"><span data-stu-id="9caf9-193">Grip the handle and remove the PCM.</span></span>
   
    ![Quitar PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="9caf9-195">**Figura 5** Quitar el PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="9caf9-196">Instalar un PCM de reemplazo</span><span class="sxs-lookup"><span data-stu-id="9caf9-196">Install a replacement PCM</span></span>
<span data-ttu-id="9caf9-197">Siga estas instrucciones para instalar un PCM en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9caf9-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="9caf9-198">Asegúrese de que insertó el módulo de batería de reserva antes de instalar el PCM de reemplazo (se aplica a los PCM de 764 W)</span><span class="sxs-lookup"><span data-stu-id="9caf9-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="9caf9-199">Para obtener más información, consulte cómo [extraer e insertar un módulo de batería de reserva](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9caf9-199">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="9caf9-200">Para instalar un PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-200">To install a PCM</span></span>
1. <span data-ttu-id="9caf9-201">Compruebe que tiene el PCM de reemplazo correcto para este gabinete.</span><span class="sxs-lookup"><span data-stu-id="9caf9-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="9caf9-202">El gabinete principal necesita un PCM de 764 W, y el gabinete EBOD necesita un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="9caf9-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="9caf9-203">No debe intentar usar el PCM de 580 W en el gabinete principal o el PCM de 764 W en el gabinete EBOD.</span><span class="sxs-lookup"><span data-stu-id="9caf9-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="9caf9-204">La siguiente imagen muestra dónde identificar esta información en la etiqueta que se anexa al PCM.</span><span class="sxs-lookup"><span data-stu-id="9caf9-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Etiqueta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="9caf9-206">**Figura 6** Etiqueta del PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="9caf9-207">Compruebe si hay daños en el gabinete, preste especial atención a los conectores.</span><span class="sxs-lookup"><span data-stu-id="9caf9-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9caf9-208">**No instale el módulo si las clavijas del conector están dobladas.**</span><span class="sxs-lookup"><span data-stu-id="9caf9-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="9caf9-209">Con el asa del PCM en posición abierta, deslice el módulo hacia el gabinete.</span><span class="sxs-lookup"><span data-stu-id="9caf9-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Instalación del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="9caf9-211">**Figura 7** Instalar el PCM</span><span class="sxs-lookup"><span data-stu-id="9caf9-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="9caf9-212">Cierre el asa del PCM manualmente.</span><span class="sxs-lookup"><span data-stu-id="9caf9-212">Manually close the PCM handle.</span></span> <span data-ttu-id="9caf9-213">Oirá un clic cuando el pestillo del asa encaje.</span><span class="sxs-lookup"><span data-stu-id="9caf9-213">You should hear a click as the handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9caf9-214">Para asegurarse de que han encajado las clavijas del conector, puede tirar suavemente del asa sin liberar el pestillo.</span><span class="sxs-lookup"><span data-stu-id="9caf9-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="9caf9-215">Si el PCM se desplaza y sale de su lugar, implica que el pestillo se cerró antes de que encajen los conectores.</span><span class="sxs-lookup"><span data-stu-id="9caf9-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   
5. <span data-ttu-id="9caf9-216">Conecte los cables de alimentación a la fuente de alimentación y el PCM.</span><span class="sxs-lookup"><span data-stu-id="9caf9-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="9caf9-217">Proteja las balas de alivio de presión.</span><span class="sxs-lookup"><span data-stu-id="9caf9-217">Secure the strain relief bales.</span></span>
7. <span data-ttu-id="9caf9-218">Encienda el PCM.</span><span class="sxs-lookup"><span data-stu-id="9caf9-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="9caf9-219">Compruebe que el reemplazo se realizó correctamente: en Azure Portal del servicio StorSimple Device Manager, vaya al dispositivo y, a continuación, a **Configuración > Supervisar > Estado del hardware**.</span><span class="sxs-lookup"><span data-stu-id="9caf9-219">Verify that the replacement was successful: in the Azure portal of your StorSimple Device Manager service, navigate to your device and then to **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="9caf9-220">En **Componentes compartidos**, el estado del PCM debe ser verde.</span><span class="sxs-lookup"><span data-stu-id="9caf9-220">Under the **Shared components**, the status of the PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9caf9-221">El PCM puede tardar unos minutos para la sustitución para inicializarse completamente.</span><span class="sxs-lookup"><span data-stu-id="9caf9-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9caf9-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9caf9-222">Next steps</span></span>
<span data-ttu-id="9caf9-223">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="9caf9-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

