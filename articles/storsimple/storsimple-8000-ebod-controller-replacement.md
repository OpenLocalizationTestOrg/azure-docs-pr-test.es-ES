---
title: Reemplazar un controlador EBOD de StorSimple 8600 | Microsoft Docs
description: "Explica cómo quitar y reemplazar uno o ambos controladores EBOD en un dispositivo de StorSimple 8600."
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
ms.openlocfilehash: 45699c267d1009c4884dd164fd3f2950d6d5f555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="b8de0-103">Reemplazar un controlador EBOD en el dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="b8de0-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="b8de0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b8de0-104">Overview</span></span>
<span data-ttu-id="b8de0-105">Este tutorial explica cómo reemplazar un módulo de controladores EBOD defectuoso en el dispositivo StorSimple de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b8de0-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="b8de0-106">Para reemplazar un módulo de controladores EBOD, necesitará:</span><span class="sxs-lookup"><span data-stu-id="b8de0-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="b8de0-107">Quitar el controlador EBOD defectuoso</span><span class="sxs-lookup"><span data-stu-id="b8de0-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="b8de0-108">Instalar un nuevo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-108">Install a new EBOD controller</span></span>

<span data-ttu-id="b8de0-109">Antes de comenzar, tenga en cuenta la siguiente información:</span><span class="sxs-lookup"><span data-stu-id="b8de0-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="b8de0-110">Los módulos EBOD vacíos deben insertarse en todas las ranuras sin usar.</span><span class="sxs-lookup"><span data-stu-id="b8de0-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="b8de0-111">El alojamiento no se refrigerará correctamente si una ranura queda abierta.</span><span class="sxs-lookup"><span data-stu-id="b8de0-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="b8de0-112">El controlador EBOD es intercambiable en caliente y puede quitarse o reemplazarse.</span><span class="sxs-lookup"><span data-stu-id="b8de0-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="b8de0-113">No quite un módulo defectuoso hasta que tenga un reemplazo.</span><span class="sxs-lookup"><span data-stu-id="b8de0-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="b8de0-114">Cuando se inicia el proceso de reemplazo, debe finalizarlo en 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="b8de0-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8de0-115">Antes de intentar quitar o reemplazar cualquier componente de StorSimple, asegúrese de revisar las [convenciones de iconos de seguridad](storsimple-safety.md#safety-icon-conventions) y otras [precauciones de seguridad](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="b8de0-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="b8de0-116">Quitar un controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-116">Remove an EBOD controller</span></span>
<span data-ttu-id="b8de0-117">Antes de reemplazar el módulo de controladores EBOD defectuoso en el dispositivo StorSimple, asegúrese de que el módulo de controladores EBOD esté activo y en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="b8de0-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="b8de0-118">El procedimiento y la tabla siguientes explican cómo quitar el módulo de controladores EBOD.</span><span class="sxs-lookup"><span data-stu-id="b8de0-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="b8de0-119">Para quitar un módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="b8de0-120">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b8de0-120">Open the Azure portal.</span></span>
2. <span data-ttu-id="b8de0-121">Navegue hasta el dispositivo y vaya a **Configuración** > **Estado de hardware** y compruebe que el estado del LED para el módulo de controladores EBOD es verde y el LED del módulo de controladores EBOD defectuoso es rojo.</span><span class="sxs-lookup"><span data-stu-id="b8de0-121">Go to your device and navigate to **Settings** > **Hardware health**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="b8de0-122">Busque el módulo de controladores EBOD defectuoso en la parte posterior del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b8de0-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="b8de0-123">Quite los cables que conectan el módulo de controladores EBOD al controlador antes de extraer el módulo EBOD del sistema.</span><span class="sxs-lookup"><span data-stu-id="b8de0-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="b8de0-124">Tome nota del puerto SAS exacto del módulo de controladores EBOD que estaba conectado al controlador.</span><span class="sxs-lookup"><span data-stu-id="b8de0-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="b8de0-125">Deberá restaurar el sistema a esta configuración después de reemplazar el módulo EBOD.</span><span class="sxs-lookup"><span data-stu-id="b8de0-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b8de0-126">Normalmente, se tratará del Puerto A, que está etiquetado como **Hospedar en** en el diagrama siguiente.</span><span class="sxs-lookup"><span data-stu-id="b8de0-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   
    ![Plano anterior del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="b8de0-128">**Figura 1** Parte posterior del módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="b8de0-129">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="b8de0-129">Label</span></span> | <span data-ttu-id="b8de0-130">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8de0-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b8de0-131">1</span><span class="sxs-lookup"><span data-stu-id="b8de0-131">1</span></span> |<span data-ttu-id="b8de0-132">LED de error</span><span class="sxs-lookup"><span data-stu-id="b8de0-132">Fault LED</span></span> |
   | <span data-ttu-id="b8de0-133">2</span><span class="sxs-lookup"><span data-stu-id="b8de0-133">2</span></span> |<span data-ttu-id="b8de0-134">LED de encendido</span><span class="sxs-lookup"><span data-stu-id="b8de0-134">Power LED</span></span> |
   | <span data-ttu-id="b8de0-135">3</span><span class="sxs-lookup"><span data-stu-id="b8de0-135">3</span></span> |<span data-ttu-id="b8de0-136">Conectores SAS</span><span class="sxs-lookup"><span data-stu-id="b8de0-136">SAS connectors</span></span> |
   | <span data-ttu-id="b8de0-137">4</span><span class="sxs-lookup"><span data-stu-id="b8de0-137">4</span></span> |<span data-ttu-id="b8de0-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="b8de0-138">SAS LEDs</span></span> |
   | <span data-ttu-id="b8de0-139">5</span><span class="sxs-lookup"><span data-stu-id="b8de0-139">5</span></span> |<span data-ttu-id="b8de0-140">Puertos en serie para uso en fábrica únicamente</span><span class="sxs-lookup"><span data-stu-id="b8de0-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="b8de0-141">6</span><span class="sxs-lookup"><span data-stu-id="b8de0-141">6</span></span> |<span data-ttu-id="b8de0-142">Puerto A (Alojar en)</span><span class="sxs-lookup"><span data-stu-id="b8de0-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="b8de0-143">7</span><span class="sxs-lookup"><span data-stu-id="b8de0-143">7</span></span> |<span data-ttu-id="b8de0-144">Puerto B (Alojar en)</span><span class="sxs-lookup"><span data-stu-id="b8de0-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="b8de0-145">8</span><span class="sxs-lookup"><span data-stu-id="b8de0-145">8</span></span> |<span data-ttu-id="b8de0-146">Puerto C (solo para uso de fábrica)</span><span class="sxs-lookup"><span data-stu-id="b8de0-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="b8de0-147">Instalar un nuevo controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-147">Install a new EBOD controller</span></span>
<span data-ttu-id="b8de0-148">El procedimiento y la tabla siguientes explican cómo instalar el módulo de controladores EBOD en el dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b8de0-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="b8de0-149">Para instalar un controlador EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="b8de0-150">Compruebe el dispositivo EBOD para ver si hay daños, especialmente en el conector de la interfaz.</span><span class="sxs-lookup"><span data-stu-id="b8de0-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="b8de0-151">No instale el nuevo controlador EBOD si alguna de las clavijas está doblada.</span><span class="sxs-lookup"><span data-stu-id="b8de0-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="b8de0-152">Con los pestillos en la posición abierta, deslice el módulo hacia el gabinete hasta que los pestillos encajen.</span><span class="sxs-lookup"><span data-stu-id="b8de0-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Instalación del controlador EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="b8de0-154">**Figura 2** Instalación del módulo de controladores EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="b8de0-155">Cierre el pestillo.</span><span class="sxs-lookup"><span data-stu-id="b8de0-155">Close the latch.</span></span> <span data-ttu-id="b8de0-156">Oirá un clic cuando el pestillo encaje.</span><span class="sxs-lookup"><span data-stu-id="b8de0-156">You should hear a click as the latch engages.</span></span>
   
    ![Liberación del pestillo EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="b8de0-158">**Figura 3** Cierre del pestillo del módulo EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="b8de0-159">Vuelva a conectar los cables.</span><span class="sxs-lookup"><span data-stu-id="b8de0-159">Reconnect the cables.</span></span> <span data-ttu-id="b8de0-160">Utilice la configuración exacta que estaba presente antes del reemplazo.</span><span class="sxs-lookup"><span data-stu-id="b8de0-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="b8de0-161">Vea la tabla y el diagrama siguientes para obtener detalles acerca de cómo conectar los cables.</span><span class="sxs-lookup"><span data-stu-id="b8de0-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Cableado del dispositivo 4U para alimentación](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="b8de0-163">**Figura 4**.</span><span class="sxs-lookup"><span data-stu-id="b8de0-163">**Figure 4**.</span></span> <span data-ttu-id="b8de0-164">Reconexión de los cables</span><span class="sxs-lookup"><span data-stu-id="b8de0-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="b8de0-165">Etiqueta</span><span class="sxs-lookup"><span data-stu-id="b8de0-165">Label</span></span> | <span data-ttu-id="b8de0-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="b8de0-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b8de0-167">1</span><span class="sxs-lookup"><span data-stu-id="b8de0-167">1</span></span> |<span data-ttu-id="b8de0-168">Receptáculo principal</span><span class="sxs-lookup"><span data-stu-id="b8de0-168">Primary enclosure</span></span> |
   | <span data-ttu-id="b8de0-169">2</span><span class="sxs-lookup"><span data-stu-id="b8de0-169">2</span></span> |<span data-ttu-id="b8de0-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b8de0-170">PCM 0</span></span> |
   | <span data-ttu-id="b8de0-171">3</span><span class="sxs-lookup"><span data-stu-id="b8de0-171">3</span></span> |<span data-ttu-id="b8de0-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b8de0-172">PCM 1</span></span> |
   | <span data-ttu-id="b8de0-173">4</span><span class="sxs-lookup"><span data-stu-id="b8de0-173">4</span></span> |<span data-ttu-id="b8de0-174">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="b8de0-174">Controller 0</span></span> |
   | <span data-ttu-id="b8de0-175">5</span><span class="sxs-lookup"><span data-stu-id="b8de0-175">5</span></span> |<span data-ttu-id="b8de0-176">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="b8de0-176">Controller 1</span></span> |
   | <span data-ttu-id="b8de0-177">6</span><span class="sxs-lookup"><span data-stu-id="b8de0-177">6</span></span> |<span data-ttu-id="b8de0-178">Controlador EBOD 0</span><span class="sxs-lookup"><span data-stu-id="b8de0-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="b8de0-179">7</span><span class="sxs-lookup"><span data-stu-id="b8de0-179">7</span></span> |<span data-ttu-id="b8de0-180">Controlador EBOD 1</span><span class="sxs-lookup"><span data-stu-id="b8de0-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="b8de0-181">8</span><span class="sxs-lookup"><span data-stu-id="b8de0-181">8</span></span> |<span data-ttu-id="b8de0-182">Receptáculo EBOD</span><span class="sxs-lookup"><span data-stu-id="b8de0-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="b8de0-183">9</span><span class="sxs-lookup"><span data-stu-id="b8de0-183">9</span></span> |<span data-ttu-id="b8de0-184">Unidades de distribución de energía</span><span class="sxs-lookup"><span data-stu-id="b8de0-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b8de0-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8de0-185">Next steps</span></span>
<span data-ttu-id="b8de0-186">Obtenga más información sobre el [Reemplazo de los componentes de hardware de StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b8de0-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

