---
title: un controlador de StorSimple EBOD aaaReplace | Documentos de Microsoft
description: "Explica cómo tooremove y reemplazar uno o ambos controladores EBOD en un dispositivo de StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="abbc4-103">Reemplazar un controlador EBOD en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="abbc4-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="abbc4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="abbc4-104">Overview</span></span>
<span data-ttu-id="abbc4-105">Este tutorial le explica cómo tooreplace un módulo de controlador EBOD defectuoso en el dispositivo de StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="abbc4-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="abbc4-106">tooreplace un módulo de controlador EBOD, necesitará:</span><span class="sxs-lookup"><span data-stu-id="abbc4-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="abbc4-107">Quitar el controlador EBOD dañado Hola</span><span class="sxs-lookup"><span data-stu-id="abbc4-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="abbc4-108">Instalar un nuevo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-108">Install a new EBOD controller</span></span>

<span data-ttu-id="abbc4-109">Considere la posibilidad de hello siguiente información antes de empezar:</span><span class="sxs-lookup"><span data-stu-id="abbc4-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="abbc4-110">Los módulos EBOD vacíos deben insertarse en todas las ranuras sin usar.</span><span class="sxs-lookup"><span data-stu-id="abbc4-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="abbc4-111">Hola alojamiento no se refrigerará correctamente si una ranura queda abierta.</span><span class="sxs-lookup"><span data-stu-id="abbc4-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="abbc4-112">controlador de EBOD Hello es intercambiable en caliente y se puede quitar o reemplazar.</span><span class="sxs-lookup"><span data-stu-id="abbc4-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="abbc4-113">No quite un módulo defectuoso hasta que tenga un reemplazo.</span><span class="sxs-lookup"><span data-stu-id="abbc4-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="abbc4-114">Cuando se inicia el proceso de reemplazo de hello, debe completarlo en el plazo de 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="abbc4-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abbc4-115">Antes de intentar tooremove o reemplace cualquier componente de StorSimple, asegúrese de que revisa hello [convenciones de iconos de seguridad](storsimple-safety.md#safety-icon-conventions) y otros [precauciones de seguridad](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="abbc4-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="abbc4-116">Quitar un controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-116">Remove an EBOD controller</span></span>
<span data-ttu-id="abbc4-117">Antes de reemplazar Hola error módulo del controlador EBOD en el dispositivo StorSimple, asegúrese de que ese Hola otro módulo de controlador EBOD esté activo y en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="abbc4-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="abbc4-118">Hello procedimiento y la tabla siguientes explican cómo tooremove Hola módulo del controlador EBOD.</span><span class="sxs-lookup"><span data-stu-id="abbc4-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="abbc4-119">tooremove un módulo de EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="abbc4-120">Hola abrir portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="abbc4-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="abbc4-121">Navegue demasiado**dispositivos** > **mantenimiento** > **estado del Hardware**y compruebe que el LED de estado de Hola de hello para Hola EBOD activo módulo de controlador está en verde y hello LED para el módulo de controlador EBOD Hola error está en rojo.</span><span class="sxs-lookup"><span data-stu-id="abbc4-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="abbc4-122">Busque el módulo del controlador EBOD de hello no se pudo en hello parte posterior del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="abbc4-123">Quite los cables de Hola que conectan el controlador toohello módulo de hello EBOD controlador antes de realizar el módulo de EBOD de hello del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="abbc4-124">Tome nota del puerto SAS exacto de Hola de módulo del controlador EBOD Hola que estaba conectado toohello controlador.</span><span class="sxs-lookup"><span data-stu-id="abbc4-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="abbc4-125">Será necesario toorestore configuración de toothis del sistema de hello después de reemplazar el módulo EBOD Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="abbc4-126">Normalmente, se trata de puerto A, que se etiqueta como **hospedar en** Hola siguiente diagrama.</span><span class="sxs-lookup"><span data-stu-id="abbc4-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![Plano anterior del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="abbc4-128">**Figura 1** Parte posterior del módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="abbc4-129">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="abbc4-129">Label</span></span> | <span data-ttu-id="abbc4-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="abbc4-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="abbc4-131">1</span><span class="sxs-lookup"><span data-stu-id="abbc4-131">1</span></span> |<span data-ttu-id="abbc4-132">LED de error</span><span class="sxs-lookup"><span data-stu-id="abbc4-132">Fault LED</span></span> |
   | <span data-ttu-id="abbc4-133">2</span><span class="sxs-lookup"><span data-stu-id="abbc4-133">2</span></span> |<span data-ttu-id="abbc4-134">LED de encendido</span><span class="sxs-lookup"><span data-stu-id="abbc4-134">Power LED</span></span> |
   | <span data-ttu-id="abbc4-135">3</span><span class="sxs-lookup"><span data-stu-id="abbc4-135">3</span></span> |<span data-ttu-id="abbc4-136">Conectores SAS</span><span class="sxs-lookup"><span data-stu-id="abbc4-136">SAS connectors</span></span> |
   | <span data-ttu-id="abbc4-137">4</span><span class="sxs-lookup"><span data-stu-id="abbc4-137">4</span></span> |<span data-ttu-id="abbc4-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="abbc4-138">SAS LEDs</span></span> |
   | <span data-ttu-id="abbc4-139">5</span><span class="sxs-lookup"><span data-stu-id="abbc4-139">5</span></span> |<span data-ttu-id="abbc4-140">Puertos en serie para uso en fábrica únicamente</span><span class="sxs-lookup"><span data-stu-id="abbc4-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="abbc4-141">6</span><span class="sxs-lookup"><span data-stu-id="abbc4-141">6</span></span> |<span data-ttu-id="abbc4-142">Puerto A (Alojar en)</span><span class="sxs-lookup"><span data-stu-id="abbc4-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="abbc4-143">7</span><span class="sxs-lookup"><span data-stu-id="abbc4-143">7</span></span> |<span data-ttu-id="abbc4-144">Puerto B (Alojar en)</span><span class="sxs-lookup"><span data-stu-id="abbc4-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="abbc4-145">8</span><span class="sxs-lookup"><span data-stu-id="abbc4-145">8</span></span> |<span data-ttu-id="abbc4-146">Puerto C (solo para uso de fábrica)</span><span class="sxs-lookup"><span data-stu-id="abbc4-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="abbc4-147">Instalar un nuevo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-147">Install a new EBOD controller</span></span>
<span data-ttu-id="abbc4-148">Hello procedimiento y la tabla siguientes explican cómo tooinstall un módulo de controlador EBOD en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="abbc4-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="abbc4-149">tooinstall un controlador de EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="abbc4-150">Compruebe hello EBOD del dispositivo si hay daños, especialmente el conector de interfaz toohello.</span><span class="sxs-lookup"><span data-stu-id="abbc4-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="abbc4-151">No instale el nuevo controlador de EBOD Hola si algún pasador está doblado.</span><span class="sxs-lookup"><span data-stu-id="abbc4-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="abbc4-152">Con bloqueos temporales de Hola Hola abra posición, módulo de diapositiva hello en el alojamiento de hello hasta Hola bloqueos se acoplen.</span><span class="sxs-lookup"><span data-stu-id="abbc4-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Instalación del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="abbc4-154">**Figura 2** instalar Hola controlador de ebod</span><span class="sxs-lookup"><span data-stu-id="abbc4-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="abbc4-155">Bloqueo de cierre Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-155">Close hello latch.</span></span> <span data-ttu-id="abbc4-156">Debe oír un clic cuando se acople el bloqueo temporal de Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-156">You should hear a click as hello latch engages.</span></span>
   
    ![Liberación del pestillo EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="abbc4-158">**Figura 3** cerrando bloqueo de módulo EBOD Hola</span><span class="sxs-lookup"><span data-stu-id="abbc4-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="abbc4-159">Vuelva a conectar los cables de Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-159">Reconnect hello cables.</span></span> <span data-ttu-id="abbc4-160">Usar configuración exacta de Hola que ya estaba presente antes de sustitución de Hola.</span><span class="sxs-lookup"><span data-stu-id="abbc4-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="abbc4-161">Vea Hola después de diagrama y de la tabla para obtener más información acerca de cómo los cables de hello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="abbc4-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Cableado del dispositivo 4U para alimentación](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="abbc4-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="abbc4-163">**Figure 4**.</span></span> <span data-ttu-id="abbc4-164">Reconexión de los cables</span><span class="sxs-lookup"><span data-stu-id="abbc4-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="abbc4-165">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="abbc4-165">Label</span></span> | <span data-ttu-id="abbc4-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="abbc4-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="abbc4-167">1</span><span class="sxs-lookup"><span data-stu-id="abbc4-167">1</span></span> |<span data-ttu-id="abbc4-168">Receptáculo principal</span><span class="sxs-lookup"><span data-stu-id="abbc4-168">Primary enclosure</span></span> |
   | <span data-ttu-id="abbc4-169">2</span><span class="sxs-lookup"><span data-stu-id="abbc4-169">2</span></span> |<span data-ttu-id="abbc4-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="abbc4-170">PCM 0</span></span> |
   | <span data-ttu-id="abbc4-171">3</span><span class="sxs-lookup"><span data-stu-id="abbc4-171">3</span></span> |<span data-ttu-id="abbc4-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="abbc4-172">PCM 1</span></span> |
   | <span data-ttu-id="abbc4-173">4</span><span class="sxs-lookup"><span data-stu-id="abbc4-173">4</span></span> |<span data-ttu-id="abbc4-174">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="abbc4-174">Controller 0</span></span> |
   | <span data-ttu-id="abbc4-175">5</span><span class="sxs-lookup"><span data-stu-id="abbc4-175">5</span></span> |<span data-ttu-id="abbc4-176">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="abbc4-176">Controller 1</span></span> |
   | <span data-ttu-id="abbc4-177">6</span><span class="sxs-lookup"><span data-stu-id="abbc4-177">6</span></span> |<span data-ttu-id="abbc4-178">Controlador EBOD 0</span><span class="sxs-lookup"><span data-stu-id="abbc4-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="abbc4-179">7</span><span class="sxs-lookup"><span data-stu-id="abbc4-179">7</span></span> |<span data-ttu-id="abbc4-180">Controlador EBOD 1</span><span class="sxs-lookup"><span data-stu-id="abbc4-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="abbc4-181">8</span><span class="sxs-lookup"><span data-stu-id="abbc4-181">8</span></span> |<span data-ttu-id="abbc4-182">Receptáculo EBOD</span><span class="sxs-lookup"><span data-stu-id="abbc4-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="abbc4-183">9</span><span class="sxs-lookup"><span data-stu-id="abbc4-183">9</span></span> |<span data-ttu-id="abbc4-184">Unidades de distribución de energía</span><span class="sxs-lookup"><span data-stu-id="abbc4-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="abbc4-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abbc4-185">Next steps</span></span>
<span data-ttu-id="abbc4-186">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="abbc4-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

