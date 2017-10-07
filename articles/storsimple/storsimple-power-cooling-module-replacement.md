---
title: aaaReplace un PCM en el dispositivo StorSimple | Documentos de Microsoft
description: "Explica cómo tooremove y reemplazar Hola de alimentación y módulo de refrigeración (PCM) en el dispositivo StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: cc19ccb29884557720f7538b90dfb05268330b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="1be80-103">Reemplazar un Módulo de alimentación y de refrigeración en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="1be80-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="1be80-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1be80-104">Overview</span></span>
<span data-ttu-id="1be80-105">Hola Power y módulo de refrigeración (PCM) en el dispositivo de StorSimple de Microsoft Azure consta de una fuente de alimentación y ventiladores de refrigeración que se controlan a través de los alojamientos EBOD y Hola principal.</span><span class="sxs-lookup"><span data-stu-id="1be80-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="1be80-106">Hay un único modelo de PCM que está certificado para cada gabinete.</span><span class="sxs-lookup"><span data-stu-id="1be80-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="1be80-107">alojamiento principal Hola está certificado para un PCM de 764 W y alojamiento de EBOD Hola está certificado para un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="1be80-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="1be80-108">Aunque hello PCM para el alojamiento principal de Hola y el alojamiento de EBOD Hola son diferentes, el procedimiento de sustitución de hello es idéntico.</span><span class="sxs-lookup"><span data-stu-id="1be80-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="1be80-109">Este tutorial explica cómo realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1be80-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="1be80-110">Quitar un PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-110">Remove a PCM</span></span>
* <span data-ttu-id="1be80-111">Instalar un PCM de reemplazo</span><span class="sxs-lookup"><span data-stu-id="1be80-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1be80-112">Antes de quitar y reemplazar un PCM, revise la información de seguridad de hello en [sustitución de componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1be80-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="1be80-113">Antes de reemplazar un PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-113">Before you replace a PCM</span></span>
<span data-ttu-id="1be80-114">Tenga en cuenta Hola después problemas importantes antes de sustituir su PCM:</span><span class="sxs-lookup"><span data-stu-id="1be80-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="1be80-115">Si Hola de alimentación de Hola se produce un error de PCM, deje instalado de módulo con hello, pero quitar el cable de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="1be80-116">ventilador de Hello continuará corriente de tooreceive de alojamiento de Hola y continuar la refrigeración adecuada de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="1be80-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="1be80-117">Si se produce un error en el ventilador de hello, Hola PCM debe toobe sustituye de forma inmediata.</span><span class="sxs-lookup"><span data-stu-id="1be80-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="1be80-118">Antes de quitar Hola PCM, desconecte power Hola Hola PCM si se desactiva el interruptor principal hello (si está presente) o retirando físicamente el cable de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="1be80-119">Esto proporciona un sistema de tooyour de advertencia que un corte del suministro es inminente.</span><span class="sxs-lookup"><span data-stu-id="1be80-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="1be80-120">Asegúrese de que ese Hola para que otro PCM es funcional continuar la operación del sistema antes de reemplazar Hola PCM con el.</span><span class="sxs-lookup"><span data-stu-id="1be80-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="1be80-121">Tan pronto como sea posible, un PCM defectuoso debe sustituirse por un PCM totalmente operativo.</span><span class="sxs-lookup"><span data-stu-id="1be80-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="1be80-122">Sustitución del módulo PCM toma solo algunos minutos toocomplete, pero debe realizarse dentro de 10 minutos de la eliminación de hello no se pudo PCM tooprevent sobrecalentamiento.</span><span class="sxs-lookup"><span data-stu-id="1be80-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="1be80-123">Tenga en cuenta que Hola reemplazo 764 W PCM los módulos enviados de fábrica de hello no contienen módulo de batería de reserva de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="1be80-124">Deberá batería de hello tooremove desde el PCM con el error y, a continuación, insertarlo en sustitución de Hola de tooperforming anterior del módulo de reemplazo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="1be80-125">Para obtener más información, vea cómo demasiado[quitar e inserte un módulo de batería de reserva](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1be80-125">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="1be80-126">Quitar un PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-126">Remove a PCM</span></span>
<span data-ttu-id="1be80-127">Siga estas instrucciones cuando esté listo tooremove una potencia y módulo de refrigeración (PCM) de su dispositivo de StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1be80-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="1be80-128">Antes de quitar el PCM, compruebe que dispone de otro correcto para sustituirlo (764 W para el alojamiento principal hello) o 580 W para hello alojamiento de EBOD.</span><span class="sxs-lookup"><span data-stu-id="1be80-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>
> 
> 

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="1be80-129">tooremove un PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-129">tooremove a PCM</span></span>
1. <span data-ttu-id="1be80-130">Hola portal de Azure clásico, haga clic en **dispositivos** > **mantenimiento** > **estado del Hardware**.</span><span class="sxs-lookup"><span data-stu-id="1be80-130">In hello Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="1be80-131">Comprobar el estado de Hola de componentes de PCM de hello en **componentes compartidos** tooidentify que ha fallado PCM:</span><span class="sxs-lookup"><span data-stu-id="1be80-131">Check hello status of hello PCM components under **Shared Components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="1be80-132">Si se produce un error en una fuente de alimentación en PCM 0, Hola estado de **fuente de alimentación en PCM 0** será rojo.</span><span class="sxs-lookup"><span data-stu-id="1be80-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="1be80-133">Si se produce un error en una fuente de alimentación en PCM 1, Hola estado de **fuente de alimentación en PCM 1** será rojo.</span><span class="sxs-lookup"><span data-stu-id="1be80-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="1be80-134">Si se produce un error de ventilador de hello en PCM 1, Hola estado **refrigeración 0 para PCM 0** o **refrigeración 1 para PCM 0** será rojo.</span><span class="sxs-lookup"><span data-stu-id="1be80-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="1be80-135">Busque Hola PCM con error en hello realizar copia del alojamiento principal Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="1be80-136">Si va a ejecutar un modelo 8600, identificar el alojamiento principal de Hola examinando Hola número de identificación de unidad de sistema se muestra en pantalla LED del panel frontal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="1be80-137">Hola predeterminado es Id. de unidad que se muestra en el alojamiento principal hello **00**, mientras que el valor predeterminado de hello Id. de unidad se muestra en hello alojamiento de EBOD es **01**.</span><span class="sxs-lookup"><span data-stu-id="1be80-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="1be80-138">Hello diagrama y la tabla siguientes explican panel frontal de Hola de pantalla de hello LED.</span><span class="sxs-lookup"><span data-stu-id="1be80-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![Identificador del sistema en el panel frontal OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="1be80-140">**Figura 1** panel frontal del dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="1be80-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="1be80-141">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="1be80-141">Label</span></span> | <span data-ttu-id="1be80-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="1be80-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1be80-143">1</span><span class="sxs-lookup"><span data-stu-id="1be80-143">1</span></span> |<span data-ttu-id="1be80-144">Botón Silencio</span><span class="sxs-lookup"><span data-stu-id="1be80-144">Mute button</span></span> |
   | <span data-ttu-id="1be80-145">2</span><span class="sxs-lookup"><span data-stu-id="1be80-145">2</span></span> |<span data-ttu-id="1be80-146">Alimentación del sistema</span><span class="sxs-lookup"><span data-stu-id="1be80-146">System power</span></span> |
   | <span data-ttu-id="1be80-147">3</span><span class="sxs-lookup"><span data-stu-id="1be80-147">3</span></span> |<span data-ttu-id="1be80-148">Error de módulo</span><span class="sxs-lookup"><span data-stu-id="1be80-148">Module fault</span></span> |
   | <span data-ttu-id="1be80-149">4</span><span class="sxs-lookup"><span data-stu-id="1be80-149">4</span></span> |<span data-ttu-id="1be80-150">Error lógico</span><span class="sxs-lookup"><span data-stu-id="1be80-150">Logical fault</span></span> |
   | <span data-ttu-id="1be80-151">5</span><span class="sxs-lookup"><span data-stu-id="1be80-151">5</span></span> |<span data-ttu-id="1be80-152">Pantalla de identificación de la unidad</span><span class="sxs-lookup"><span data-stu-id="1be80-152">Unit ID display</span></span> |
3. <span data-ttu-id="1be80-153">Hola LED indicador Hola parte posterior del alojamiento principal Hola de supervisión también puede utilizarse tooidentify Hola PCM con el error.</span><span class="sxs-lookup"><span data-stu-id="1be80-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="1be80-154">Vea Hola siguiente diagrama y tabla toounderstand cómo toouse Hola LED toolocate Hola PCM con el error.</span><span class="sxs-lookup"><span data-stu-id="1be80-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="1be80-155">Por ejemplo, si hello LED correspondiente toohello **error de ventilador** está encendido, ventilador Hola ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="1be80-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="1be80-156">Del mismo modo, si hello LED correspondiente demasiado**error de CA** está encendido, fuente de alimentación de hello ha producido un error.</span><span class="sxs-lookup"><span data-stu-id="1be80-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Backplane de LED indicadores de supervisión del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="1be80-158">**Figura 2** Parte posterior del PCM con LED indicadores</span><span class="sxs-lookup"><span data-stu-id="1be80-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="1be80-159">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="1be80-159">Label</span></span> | <span data-ttu-id="1be80-160">Descripción</span><span class="sxs-lookup"><span data-stu-id="1be80-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1be80-161">1</span><span class="sxs-lookup"><span data-stu-id="1be80-161">1</span></span> |<span data-ttu-id="1be80-162">Error de corriente alterna</span><span class="sxs-lookup"><span data-stu-id="1be80-162">AC power failure</span></span> |
   | <span data-ttu-id="1be80-163">2</span><span class="sxs-lookup"><span data-stu-id="1be80-163">2</span></span> |<span data-ttu-id="1be80-164">Error del ventilador</span><span class="sxs-lookup"><span data-stu-id="1be80-164">Fan failure</span></span> |
   | <span data-ttu-id="1be80-165">3</span><span class="sxs-lookup"><span data-stu-id="1be80-165">3</span></span> |<span data-ttu-id="1be80-166">Error de la batería</span><span class="sxs-lookup"><span data-stu-id="1be80-166">Battery fault</span></span> |
   | <span data-ttu-id="1be80-167">4</span><span class="sxs-lookup"><span data-stu-id="1be80-167">4</span></span> |<span data-ttu-id="1be80-168">PCM correcto</span><span class="sxs-lookup"><span data-stu-id="1be80-168">PCM OK</span></span> |
   | <span data-ttu-id="1be80-169">5</span><span class="sxs-lookup"><span data-stu-id="1be80-169">5</span></span> |<span data-ttu-id="1be80-170">Error de alimentación de CD</span><span class="sxs-lookup"><span data-stu-id="1be80-170">DC power failure</span></span> |
   | <span data-ttu-id="1be80-171">6</span><span class="sxs-lookup"><span data-stu-id="1be80-171">6</span></span> |<span data-ttu-id="1be80-172">Batería en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="1be80-172">Battery healthy</span></span> |
4. <span data-ttu-id="1be80-173">Consulte toohello siguiente diagrama de hello parte posterior del módulo PCM en hello StorSimple dispositivo toolocate Hola error.</span><span class="sxs-lookup"><span data-stu-id="1be80-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="1be80-174">PCM 0 está a la izquierda de Hola y PCM 1 consiste en hello derecho.</span><span class="sxs-lookup"><span data-stu-id="1be80-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="1be80-175">tabla de Hello siguiente explica los módulos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-175">hello table that follows explains hello modules.</span></span>
   
     ![Backplane de módulos del gabinete principal del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="1be80-177">**Figura 3** Parte posterior de dispositivo con módulos de complementos</span><span class="sxs-lookup"><span data-stu-id="1be80-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="1be80-178">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="1be80-178">Label</span></span> | <span data-ttu-id="1be80-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="1be80-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1be80-180">1</span><span class="sxs-lookup"><span data-stu-id="1be80-180">1</span></span> |<span data-ttu-id="1be80-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="1be80-181">PCM 0</span></span> |
   | <span data-ttu-id="1be80-182">2</span><span class="sxs-lookup"><span data-stu-id="1be80-182">2</span></span> |<span data-ttu-id="1be80-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="1be80-183">PCM 1</span></span> |
   | <span data-ttu-id="1be80-184">3</span><span class="sxs-lookup"><span data-stu-id="1be80-184">3</span></span> |<span data-ttu-id="1be80-185">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="1be80-185">Controller 0</span></span> |
   | <span data-ttu-id="1be80-186">4</span><span class="sxs-lookup"><span data-stu-id="1be80-186">4</span></span> |<span data-ttu-id="1be80-187">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="1be80-187">Controller 1</span></span> |
5. <span data-ttu-id="1be80-188">Activar Hola PCM con el error y desconecte la fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="1be80-189">Ahora puede quitar Hola PCM.</span><span class="sxs-lookup"><span data-stu-id="1be80-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="1be80-190">Tome los bloqueos temporales de Hola y Hola de hello PCM controlar entre el pulgar y el índice y apriételos identificador de hello tooopen juntos.</span><span class="sxs-lookup"><span data-stu-id="1be80-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Abrir el asa del PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="1be80-192">**Figura 4** controlar Hola de apertura PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="1be80-193">Agarre el identificador hello y quite Hola PCM.</span><span class="sxs-lookup"><span data-stu-id="1be80-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Quitar PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="1be80-195">**Figura 5** Removing Hola PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="1be80-196">Instalar un PCM de reemplazo</span><span class="sxs-lookup"><span data-stu-id="1be80-196">Install a replacement PCM</span></span>
<span data-ttu-id="1be80-197">Siga estos tooinstall instrucciones un PCM en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1be80-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="1be80-198">Asegúrese de que haya insertado Hola batería de reserva módulo anterior tooinstalling Hola PCM de sustitución (se aplica solo PCM W de too764).</span><span class="sxs-lookup"><span data-stu-id="1be80-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="1be80-199">Para obtener más información, vea cómo demasiado[quitar e inserte un módulo de batería de reserva](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1be80-199">For more information, see how too[remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="1be80-200">tooinstall un PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="1be80-201">Compruebe que dispone de hello PCM de reemplazo correcto para este alojamiento.</span><span class="sxs-lookup"><span data-stu-id="1be80-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="1be80-202">alojamiento principal Hola necesita un PCM de 764 W y Hola alojamiento de EBOD necesita un PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="1be80-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="1be80-203">No debería intentar toouse Hola PCM de 580 W alojamiento principal de Hola u Hola PCM de 764 W Hola alojamiento de EBOD.</span><span class="sxs-lookup"><span data-stu-id="1be80-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="1be80-204">Hola siguiente imagen muestra donde tooidentify esta información en hello decir etiqueta pegada toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="1be80-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Etiqueta del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="1be80-206">**Figura 6** Etiqueta del PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="1be80-207">Busque el alojamiento de toohello de daños, prestando especial atención toohello conectores.</span><span class="sxs-lookup"><span data-stu-id="1be80-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1be80-208">**No instale el módulo de hello si algún pasador del conector está doblado.**</span><span class="sxs-lookup"><span data-stu-id="1be80-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="1be80-209">Con hello PCM controlar Hola abra posición, módulo de diapositiva hello en el alojamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Instalación del PCM del dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="1be80-211">**Figura 7** instalar Hola PCM</span><span class="sxs-lookup"><span data-stu-id="1be80-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="1be80-212">Cierre manualmente el asa del PCM Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="1be80-213">Debe oír un clic cuando se acople el cierre del asa Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-213">You should hear a click as hello handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1be80-214">tooensure que Hola patillas de conexión se han acoplado, puede tirar suavemente en hello identificador sin liberar el bloqueo temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="1be80-215">Si Hola PCM se desliza hacia afuera, se referirá a que ese bloqueo Hola se cerró antes de conectores de hello ocupado.</span><span class="sxs-lookup"><span data-stu-id="1be80-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="1be80-216">Conecte la fuente de alimentación de toohello de cables de alimentación de Hola y toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="1be80-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="1be80-217">Proteger una demanda Hola balas de relieve.</span><span class="sxs-lookup"><span data-stu-id="1be80-217">Secure hello strain relief bales.</span></span> 
7. <span data-ttu-id="1be80-218">Activar Hola PCM.</span><span class="sxs-lookup"><span data-stu-id="1be80-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="1be80-219">Reemplazo de hello fue correcta: Hola portal de Azure clásico de su servicio StorSimple Manager, navegue demasiado**dispositivos** > **mantenimiento**  >  **Estado del hardware**.</span><span class="sxs-lookup"><span data-stu-id="1be80-219">Verify that hello replacement was successful: in hello Azure classic portal of your StorSimple Manager service, navigate too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="1be80-220">En **componentes compartidos**, estado de Hola de hello PCM debe ser verde.</span><span class="sxs-lookup"><span data-stu-id="1be80-220">Under **Shared Components**, hello status of hello PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1be80-221">Puede tardar unos minutos para la inicialización de toocompletely PCM de reemplazo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1be80-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="1be80-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1be80-222">Next steps</span></span>
<span data-ttu-id="1be80-223">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="1be80-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

