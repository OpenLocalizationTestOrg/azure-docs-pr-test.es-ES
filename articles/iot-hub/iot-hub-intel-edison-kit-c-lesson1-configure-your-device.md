---
title: "Conexión de Intel Edison (C) a Azure IoT: Lección 1: Configuración del dispositivo | Microsoft Docs"
description: Configure Intel Edison para usarlo por primera vez.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configuración de Arduino, conexión de Arduino al equipo, configuración de Arduino, placa Arduino"
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
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="96f36-104">Configuración de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="96f36-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="96f36-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="96f36-105">What you will do</span></span>
<span data-ttu-id="96f36-106">Configure Intel Edison para usarlo por primera vez ensamblando la placa, encendiéndola e instalando la herramienta de configuración en el sistema operativo de escritorio. El objetivo es actualizar el firmware de Edison, establecer su contraseña y conectarlo a una red Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="96f36-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="96f36-107">Si tiene problemas, busque soluciones en [esta página][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="96f36-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="96f36-108">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="96f36-108">What you will learn</span></span>
<span data-ttu-id="96f36-109">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="96f36-109">In this article, you will learn:</span></span>

* <span data-ttu-id="96f36-110">Cómo ensamblar la placa Edison y encenderla.</span><span class="sxs-lookup"><span data-stu-id="96f36-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="96f36-111">Cómo actualizar el firmware de Edison, establecer la contraseña y conectarse a una red Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="96f36-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="96f36-112">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="96f36-112">What you need</span></span>
<span data-ttu-id="96f36-113">Para completar esta operación, necesita las siguientes piezas del kit de inicio de Intel Edison:</span><span class="sxs-lookup"><span data-stu-id="96f36-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="96f36-114">El módulo Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="96f36-114">Intel® Edison module</span></span>
* <span data-ttu-id="96f36-115">La placa de expansión de Arduino.</span><span class="sxs-lookup"><span data-stu-id="96f36-115">Arduino expansion board</span></span>
* <span data-ttu-id="96f36-116">Cualquiera de las piezas intermedias o los tornillos incluidos en el paquete, por ejemplo, los dos tornillos para fijar el módulo a la placa de expansión y los cuatro conjuntos de tornillos y separadores de plástico.</span><span class="sxs-lookup"><span data-stu-id="96f36-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="96f36-117">Un cable USB Micro B a Tipo A.</span><span class="sxs-lookup"><span data-stu-id="96f36-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="96f36-118">Una fuente de alimentación de corriente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="96f36-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="96f36-119">La fuente de alimentación debe ser del siguiente tipo:</span><span class="sxs-lookup"><span data-stu-id="96f36-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="96f36-120">7-15 V CC.</span><span class="sxs-lookup"><span data-stu-id="96f36-120">7-15V DC</span></span>
  - <span data-ttu-id="96f36-121">Un mínimo de 1500 mA.</span><span class="sxs-lookup"><span data-stu-id="96f36-121">At least 1500mA</span></span>
  - <span data-ttu-id="96f36-122">La clavija central o interna debe ser el polo positivo de la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="96f36-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Los elementos del kit de inicio](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="96f36-124">También necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="96f36-124">You also need:</span></span>

* <span data-ttu-id="96f36-125">Un equipo con Windows, Mac o Linux.</span><span class="sxs-lookup"><span data-stu-id="96f36-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="96f36-126">Una conexión inalámbrica para establecer conexión entre Edison y el equipo.</span><span class="sxs-lookup"><span data-stu-id="96f36-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="96f36-127">Una conexión a Internet para descargar la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="96f36-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="96f36-128">Ensamblaje de la placa</span><span class="sxs-lookup"><span data-stu-id="96f36-128">Assemble your board</span></span>

<span data-ttu-id="96f36-129">En esta sección encontrará los pasos necesarios para conectar el módulo Intel® Edison a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="96f36-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="96f36-130">Coloque el módulo Intel® Edison dentro del contorno blanco de la placa de expansión, de forma que los agujeros del módulo queden alineados con los tornillos de la placa expansión.</span><span class="sxs-lookup"><span data-stu-id="96f36-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="96f36-131">Presione hacia abajo en el módulo, justo debajo de la frase `What will you make?`, hasta que oiga un chasquido.</span><span class="sxs-lookup"><span data-stu-id="96f36-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="96f36-133">Utilice las dos tuercas hexagonales (incluidas en el paquete) para fijar el módulo a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="96f36-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="96f36-135">Inserte un tornillo en uno de los cuatro agujeros de las esquinas de la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="96f36-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="96f36-136">Gire y apriete uno de los separadores de plástico blancos sobre el tornillo.</span><span class="sxs-lookup"><span data-stu-id="96f36-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="96f36-138">Repita el paso anterior con los otros tres separadores de las esquinas.</span><span class="sxs-lookup"><span data-stu-id="96f36-138">Repeat for the other three corner spacers.</span></span>

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="96f36-140">Ya ha ensamblado la placa.</span><span class="sxs-lookup"><span data-stu-id="96f36-140">Now your board is assembled.</span></span>

   ![Placa ensamblada](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="96f36-142">Encendido de Edison</span><span class="sxs-lookup"><span data-stu-id="96f36-142">Power up Edison</span></span>

1. <span data-ttu-id="96f36-143">Conecte la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="96f36-143">Plug in the power supply.</span></span>

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="96f36-145">Un LED verde (con la etiqueta DS1 en la placa de expansión de Arduino*) debería encenderse y permanecer encendido.</span><span class="sxs-lookup"><span data-stu-id="96f36-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="96f36-146">Espere un minuto para que termine de inicializarse la placa.</span><span class="sxs-lookup"><span data-stu-id="96f36-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="96f36-147">Si no tiene una fuente de alimentación de CC, puede encenderla usando un puerto USB.</span><span class="sxs-lookup"><span data-stu-id="96f36-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="96f36-148">Consulte la sección `Connect Edison to your computer` para más información.</span><span class="sxs-lookup"><span data-stu-id="96f36-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="96f36-149">La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.</span><span class="sxs-lookup"><span data-stu-id="96f36-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="96f36-150">Conexión de Edison a un equipo</span><span class="sxs-lookup"><span data-stu-id="96f36-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="96f36-151">Mueva hacia abajo el microconmutador (es decir, hacia los dos puertos microUSB) para activar el modo de dispositivo de Edison.</span><span class="sxs-lookup"><span data-stu-id="96f36-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="96f36-152">Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="96f36-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Desplazamiento hacia abajo del microconmutador](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="96f36-154">Conecte el cable microUSB al puerto microUSB superior.</span><span class="sxs-lookup"><span data-stu-id="96f36-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Puerto microUSB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="96f36-156">Conecte el otro extremo del cable USB al equipo.</span><span class="sxs-lookup"><span data-stu-id="96f36-156">Plug the other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="96f36-158">Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).</span><span class="sxs-lookup"><span data-stu-id="96f36-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="96f36-159">Descarga y ejecución de la herramienta de configuración</span><span class="sxs-lookup"><span data-stu-id="96f36-159">Download and run the configuration tool</span></span>
<span data-ttu-id="96f36-160">Obtenga la herramienta de configuración más reciente haciendo clic [aquí](https://software.intel.com/en-us/iot/hardware/edison/downloads) (los vínculos se encuentran bajo el título `Installers`).</span><span class="sxs-lookup"><span data-stu-id="96f36-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="96f36-161">Ejecute la herramienta y siga las instrucciones que aparecen en pantalla. Vaya haciendo clic en Next (Siguiente) según proceda.</span><span class="sxs-lookup"><span data-stu-id="96f36-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="96f36-162">Actualización del firmware</span><span class="sxs-lookup"><span data-stu-id="96f36-162">Flash firmware</span></span>
1. <span data-ttu-id="96f36-163">En la página `Set up options`, haga clic en `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="96f36-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="96f36-164">Seleccione la imagen que se instalará en la placa realizando una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="96f36-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="96f36-165">Para descargar e instalar en la placa la imagen del firmware más reciente de Intel, seleccione `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="96f36-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="96f36-166">Para actualizar el firmware de la placa con una imagen que ya ha guardado en el equipo, seleccione `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="96f36-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="96f36-167">Busque y seleccione la imagen con la que va a actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="96f36-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="96f36-168">La herramienta de instalación tratará de actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="96f36-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="96f36-169">La duración del proceso puede ser de hasta 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="96f36-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="96f36-170">Establecimiento de la contraseña</span><span class="sxs-lookup"><span data-stu-id="96f36-170">Set password</span></span>
1. <span data-ttu-id="96f36-171">En la página `Set up options`, haga clic en `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="96f36-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="96f36-172">Puede establecer un nombre personalizado para la placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="96f36-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="96f36-173">Esto es opcional.</span><span class="sxs-lookup"><span data-stu-id="96f36-173">This is optional.</span></span>
3. <span data-ttu-id="96f36-174">Escriba una contraseña para la placa y, luego, haga clic en `Set password`.</span><span class="sxs-lookup"><span data-stu-id="96f36-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="96f36-175">Anote la contraseña, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="96f36-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="96f36-176">Conexión a una red Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="96f36-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="96f36-177">En la página `Set up options`, haga clic en `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="96f36-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="96f36-178">Espere, como máximo, un minuto, ya que el equipo buscará las redes Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="96f36-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="96f36-179">En la lista desplegable `Detected Networks`, seleccione su red.</span><span class="sxs-lookup"><span data-stu-id="96f36-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="96f36-180">En la lista desplegable `Security`, seleccione el tipo de seguridad de la red.</span><span class="sxs-lookup"><span data-stu-id="96f36-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="96f36-181">Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="96f36-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="96f36-182">Anote la dirección IP, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="96f36-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="96f36-183">Asegúrese de que Edison se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="96f36-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="96f36-184">El equipo se conectará a Edison mediante la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="96f36-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="96f36-185">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="96f36-185">Congratulations!</span></span> <span data-ttu-id="96f36-186">Ha configurado correctamente Edison.</span><span class="sxs-lookup"><span data-stu-id="96f36-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="96f36-187">Resumen</span><span class="sxs-lookup"><span data-stu-id="96f36-187">Summary</span></span>
<span data-ttu-id="96f36-188">En este artículo ha aprendido a ensamblar la placa Edison, actualizar su firmware, configurar la contraseña y conectar la placa a una red Wi-Fi mediante la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="96f36-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="96f36-189">Tenga en cuenta que todavía el LED no se encenderá.</span><span class="sxs-lookup"><span data-stu-id="96f36-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="96f36-190">En la siguiente tarea, instalará las herramientas y el software necesarios como preparativo para ejecutar una aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="96f36-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f36-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="96f36-191">Next steps</span></span>
<span data-ttu-id="96f36-192">[Obtención de las herramientas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="96f36-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md