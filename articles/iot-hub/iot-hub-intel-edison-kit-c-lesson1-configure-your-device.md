---
title: "Connect Intel Edison (C) tooAzure IoT - lección 1: Configurar dispositivo | Documentos de Microsoft"
description: Configure Intel Edison para usarlo por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurar, conectar arduino toopc, el programa de instalación arduino, panel de arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="8f970-104">Configuración de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="8f970-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8f970-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="8f970-105">What you will do</span></span>
<span data-ttu-id="8f970-106">Configurar a Intel Edison para usarlos por primera vez ensamblando panel hello, activando la e instalación tooyour de herramienta de configuración de escritorio tooflash de SO firmware Edison, establecer su contraseña y conéctelo tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8f970-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="8f970-107">Si tiene problemas, buscar soluciones en hello [solución de problemas de página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8f970-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8f970-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="8f970-108">What you will learn</span></span>
<span data-ttu-id="8f970-109">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f970-109">In this article, you will learn:</span></span>

* <span data-ttu-id="8f970-110">¿Cómo tooassemble Edison del panel y enciéndalo.</span><span class="sxs-lookup"><span data-stu-id="8f970-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="8f970-111">Cómo firmware tooflash Edison, establecer contraseña y conectarse Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8f970-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f970-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8f970-112">What you need</span></span>
<span data-ttu-id="8f970-113">toocomplete esta operación, necesita Hola siguientes partes de su Intel Edison Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="8f970-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="8f970-114">El módulo Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="8f970-114">Intel® Edison module</span></span>
* <span data-ttu-id="8f970-115">La placa de expansión de Arduino.</span><span class="sxs-lookup"><span data-stu-id="8f970-115">Arduino expansion board</span></span>
* <span data-ttu-id="8f970-116">Las barras de separación o tornillos incluidos en el empaquetado de hello, incluida la tarjeta de expansión de dos tornillos toofasten Hola módulo toohello y cuatro conjuntos de tornillos y separadores de plástico.</span><span class="sxs-lookup"><span data-stu-id="8f970-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="8f970-117">Un cable USB A tooType de Micro B</span><span class="sxs-lookup"><span data-stu-id="8f970-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="8f970-118">Una fuente de alimentación de corriente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="8f970-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="8f970-119">La fuente de alimentación debe ser del siguiente tipo:</span><span class="sxs-lookup"><span data-stu-id="8f970-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="8f970-120">7-15 V CC.</span><span class="sxs-lookup"><span data-stu-id="8f970-120">7-15V DC</span></span>
  - <span data-ttu-id="8f970-121">Un mínimo de 1500 mA.</span><span class="sxs-lookup"><span data-stu-id="8f970-121">At least 1500mA</span></span>
  - <span data-ttu-id="8f970-122">pin de Hello center o interna debe ser polo positivo de Hola Hola de fuente de alimentación</span><span class="sxs-lookup"><span data-stu-id="8f970-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Los elementos del kit de inicio](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="8f970-124">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8f970-124">You also need:</span></span>

* <span data-ttu-id="8f970-125">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="8f970-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="8f970-126">Una conexión inalámbrica para tooconnect Edison a.</span><span class="sxs-lookup"><span data-stu-id="8f970-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="8f970-127">Una herramienta de configuración de toodownload de conexión de Internet.</span><span class="sxs-lookup"><span data-stu-id="8f970-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="8f970-128">Ensamblaje de la placa</span><span class="sxs-lookup"><span data-stu-id="8f970-128">Assemble your board</span></span>

<span data-ttu-id="8f970-129">Esta sección contiene pasos tooattach su tarjeta de expansión de Intel® Edison módulo tooyour.</span><span class="sxs-lookup"><span data-stu-id="8f970-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="8f970-130">Coloque el módulo de Intel® Edison de hello en esquema Hola blanco en su tarjeta de expansión, se alinea vulnerabilidades de hello en el módulo de hello con tornillos de hello en la tarjeta de expansión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="8f970-131">Mantenga presionada en módulo de hello justo debajo de palabras de hello `What will you make?` hasta que cree un complemento.</span><span class="sxs-lookup"><span data-stu-id="8f970-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="8f970-133">Utilice Hola dos frutos hexadecimal (incluidos en el paquete de hello) toosecure Hola módulo toohello expansión placa.</span><span class="sxs-lookup"><span data-stu-id="8f970-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="8f970-135">Inserte un tornillo en uno de cuatro agujeros de esquina hello en la tarjeta de expansión de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="8f970-136">Retorcer y apriete uno de los separadores de plástico blanco hello en tornillo Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="8f970-138">Repita este paso para Hola otros separadores de esquina de tres.</span><span class="sxs-lookup"><span data-stu-id="8f970-138">Repeat for hello other three corner spacers.</span></span>

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="8f970-140">Ya ha ensamblado la placa.</span><span class="sxs-lookup"><span data-stu-id="8f970-140">Now your board is assembled.</span></span>

   ![Placa ensamblada](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="8f970-142">Encendido de Edison</span><span class="sxs-lookup"><span data-stu-id="8f970-142">Power up Edison</span></span>

1. <span data-ttu-id="8f970-143">Conecte en fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-143">Plug in hello power supply.</span></span>

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="8f970-145">Un LED verde (con la etiqueta DS1 en hello tarjeta de expansión Arduino *) debe encenderse y permanecer encendido.</span><span class="sxs-lookup"><span data-stu-id="8f970-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="8f970-146">Espere un minuto para hello panel toofinish arrancado.</span><span class="sxs-lookup"><span data-stu-id="8f970-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f970-147">Si no tiene una fuente de alimentación de controlador de dominio, puede placa de Hola de alimentación a través de un puerto USB.</span><span class="sxs-lookup"><span data-stu-id="8f970-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="8f970-148">Consulte la sección `Connect Edison tooyour computer` para más información.</span><span class="sxs-lookup"><span data-stu-id="8f970-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="8f970-149">La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.</span><span class="sxs-lookup"><span data-stu-id="8f970-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="8f970-150">Conectar Edison tooyour equipo</span><span class="sxs-lookup"><span data-stu-id="8f970-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="8f970-151">Alternar hacia abajo Hola microconmutador hacia Hola dos micro puertos USB para que Edison está en modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8f970-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="8f970-152">Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="8f970-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Alternar hacia abajo microconmutador Hola](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="8f970-154">Enchufe cable USB micro de hello en puerto USB de micro superior Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Puerto microUSB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="8f970-156">Plug Hola otro extremo del cable USB en el equipo.</span><span class="sxs-lookup"><span data-stu-id="8f970-156">Plug hello other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="8f970-158">Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).</span><span class="sxs-lookup"><span data-stu-id="8f970-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="8f970-159">Descargue y ejecute la herramienta de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="8f970-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="8f970-160">Obtener la herramienta de configuración más reciente de Hola de [este vínculo](https://software.intel.com/en-us/iot/hardware/edison/downloads) aparecen en hello `Installers` encabezado.</span><span class="sxs-lookup"><span data-stu-id="8f970-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="8f970-161">Ejecutar la herramienta de Hola y siga su pantalla instrucciones, hacer clic en siguiente cuando sea necesario</span><span class="sxs-lookup"><span data-stu-id="8f970-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="8f970-162">Actualización del firmware</span><span class="sxs-lookup"><span data-stu-id="8f970-162">Flash firmware</span></span>
1. <span data-ttu-id="8f970-163">En hello `Set up options` página, haga clic en `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="8f970-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="8f970-164">Seleccione tooflash de imagen de hello en el panel, realice uno de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="8f970-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="8f970-165">toodownload y flash, seleccione el panel con la imagen de firmware más reciente de hello disponible de Intel, `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="8f970-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="8f970-166">Seleccione el panel con una imagen que ya se ha guardado en el equipo de tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="8f970-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="8f970-167">Busque la imagen de hello seleccione tooand desea tooflash tooyour panel.</span><span class="sxs-lookup"><span data-stu-id="8f970-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="8f970-168">herramienta de configuración de Hello intentará tooflash el panel.</span><span class="sxs-lookup"><span data-stu-id="8f970-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="8f970-169">todo el proceso intermitente Hola puede tardar minutos too10.</span><span class="sxs-lookup"><span data-stu-id="8f970-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="8f970-170">Establecimiento de la contraseña</span><span class="sxs-lookup"><span data-stu-id="8f970-170">Set password</span></span>
1. <span data-ttu-id="8f970-171">En hello `Set up options` página, haga clic en `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="8f970-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="8f970-172">Puede establecer un nombre personalizado para la placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="8f970-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="8f970-173">Esto es opcional.</span><span class="sxs-lookup"><span data-stu-id="8f970-173">This is optional.</span></span>
3. <span data-ttu-id="8f970-174">Escriba una contraseña para la placa y, luego, haga clic en `Set password`.</span><span class="sxs-lookup"><span data-stu-id="8f970-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="8f970-175">Marcar como inactiva la contraseña de hello, que se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="8f970-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="8f970-176">Conexión a una red Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="8f970-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="8f970-177">En hello `Set up options` página, haga clic en `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="8f970-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="8f970-178">Espera tooone minuto como los análisis del equipo para las redes Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="8f970-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="8f970-179">De hello `Detected Networks` lista desplegable, seleccione la red.</span><span class="sxs-lookup"><span data-stu-id="8f970-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="8f970-180">De hello `Security` lista desplegable, tipo de seguridad de la red de hello select.</span><span class="sxs-lookup"><span data-stu-id="8f970-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="8f970-181">Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="8f970-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="8f970-182">Marcar como inactiva Hola dirección IP, que se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="8f970-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="8f970-183">Asegúrese de que ese Edison está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="8f970-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="8f970-184">El equipo conecta tooyour Edison utilizando la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="8f970-185">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="8f970-185">Congratulations!</span></span> <span data-ttu-id="8f970-186">Ha configurado correctamente Edison.</span><span class="sxs-lookup"><span data-stu-id="8f970-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="8f970-187">Resumen</span><span class="sxs-lookup"><span data-stu-id="8f970-187">Summary</span></span>
<span data-ttu-id="8f970-188">En este artículo, ha aprendido cómo tooassemble Hola panel Edison, flash su firmware, la contraseña de la instalación y conéctelo tooWi-Fi mediante la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="8f970-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="8f970-189">Tenga en cuenta que Hola que LED aún no ilumina.</span><span class="sxs-lookup"><span data-stu-id="8f970-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="8f970-190">Hola siguiente tarea es software como preparación para ejecutar una aplicación de ejemplo en Edison y herramientas que necesitan tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="8f970-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f970-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f970-191">Next steps</span></span>
<span data-ttu-id="8f970-192">[Obtener herramientas de Hola][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="8f970-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md