---
title: 'Intel Edison en la nube (Node.js): Conectar Intel Edison a Azure IoT Hub | Microsoft Docs'
description: "Con este tutorial aprenderá a configurar y conectar Intel Edison a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: azure iot intel edison, intel edison iot hub, intel edison enviar datos a la nube, intel edison en la nube
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5a31efba704045196b5563f7bc467c773bea7805
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-nodejs"></a><span data-ttu-id="588e0-104">Conectar Intel Edison a Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="588e0-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="588e0-105">En este tutorial, empiece por aprender los conceptos básicos sobre cómo trabajar con Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="588e0-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="588e0-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="588e0-107">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="588e0-107">Don't have a kit yet?</span></span> <span data-ttu-id="588e0-108">Comience [aquí](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="588e0-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="588e0-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="588e0-109">What you do</span></span>

* <span data-ttu-id="588e0-110">Configure Intel Edison y los módulos de Grove.</span><span class="sxs-lookup"><span data-stu-id="588e0-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="588e0-111">Cree un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-111">Create an IoT hub.</span></span>
* <span data-ttu-id="588e0-112">Registre un dispositivo para Edison en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="588e0-113">Ejecute una aplicación de ejemplo en Edison para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="588e0-114">Conecte Intel Edison al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="588e0-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="588e0-115">Luego ejecute una aplicación de ejemplo en Edison para recopilar datos de temperatura y humedad de un sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="588e0-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="588e0-116">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="588e0-117">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="588e0-117">What you learn</span></span>

* <span data-ttu-id="588e0-118">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="588e0-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="588e0-119">Cómo conectar Edison a un sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="588e0-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="588e0-120">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="588e0-121">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="588e0-122">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="588e0-122">What you need</span></span>

![Lo que necesita](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="588e0-124">La placa de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="588e0-124">The Intel Edison board</span></span>
* <span data-ttu-id="588e0-125">La placa de expansión de Arduino.</span><span class="sxs-lookup"><span data-stu-id="588e0-125">Arduino expansion board</span></span>
* <span data-ttu-id="588e0-126">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="588e0-126">An active Azure subscription.</span></span> <span data-ttu-id="588e0-127">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="588e0-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="588e0-128">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="588e0-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="588e0-129">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="588e0-129">An Internet connection.</span></span>
* <span data-ttu-id="588e0-130">Un cable USB Micro B a Tipo A.</span><span class="sxs-lookup"><span data-stu-id="588e0-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="588e0-131">Una fuente de alimentación de corriente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="588e0-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="588e0-132">La fuente de alimentación debe ser del siguiente tipo:</span><span class="sxs-lookup"><span data-stu-id="588e0-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="588e0-133">7-15 V CC.</span><span class="sxs-lookup"><span data-stu-id="588e0-133">7-15V DC</span></span>
  - <span data-ttu-id="588e0-134">Un mínimo de 1500 mA.</span><span class="sxs-lookup"><span data-stu-id="588e0-134">At least 1500mA</span></span>
  - <span data-ttu-id="588e0-135">La clavija central o interna debe ser el polo positivo de la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="588e0-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="588e0-136">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="588e0-136">The following items are optional:</span></span>

* <span data-ttu-id="588e0-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="588e0-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="588e0-138">Grove: sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="588e0-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="588e0-139">Cable de Grove</span><span class="sxs-lookup"><span data-stu-id="588e0-139">Grove Cable</span></span>
* <span data-ttu-id="588e0-140">Cualquiera de las piezas intermedias o los tornillos incluidos en el paquete, por ejemplo, los dos tornillos para fijar el módulo a la placa de expansión y los cuatro conjuntos de tornillos y separadores de plástico.</span><span class="sxs-lookup"><span data-stu-id="588e0-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="588e0-141">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="588e0-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="588e0-142">Configurar Intel Edison</span><span class="sxs-lookup"><span data-stu-id="588e0-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="588e0-143">Ensamblaje de la placa</span><span class="sxs-lookup"><span data-stu-id="588e0-143">Assemble your board</span></span>

<span data-ttu-id="588e0-144">En esta sección encontrará los pasos necesarios para conectar el módulo Intel® Edison a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="588e0-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="588e0-145">Coloque el módulo Intel® Edison dentro del contorno blanco de la placa de expansión, de forma que los agujeros del módulo queden alineados con los tornillos de la placa expansión.</span><span class="sxs-lookup"><span data-stu-id="588e0-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="588e0-146">Presione hacia abajo en el módulo, justo debajo de la frase `What will you make?`, hasta que oiga un chasquido.</span><span class="sxs-lookup"><span data-stu-id="588e0-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="588e0-148">Utilice las dos tuercas hexagonales (incluidas en el paquete) para fijar el módulo a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="588e0-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="588e0-150">Inserte un tornillo en uno de los cuatro agujeros de las esquinas de la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="588e0-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="588e0-151">Gire y apriete uno de los separadores de plástico blancos sobre el tornillo.</span><span class="sxs-lookup"><span data-stu-id="588e0-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="588e0-153">Repita el paso anterior con los otros tres separadores de las esquinas.</span><span class="sxs-lookup"><span data-stu-id="588e0-153">Repeat for the other three corner spacers.</span></span>

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="588e0-155">Ya ha ensamblado la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-155">Now your board is assembled.</span></span>

   ![Placa ensamblada](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="588e0-157">Conectar Grove Base Shield y el sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="588e0-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="588e0-158">Coloque Grove Base Shield en la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="588e0-159">Asegúrese de que todas las patillas estén bien conectadas a la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="588e0-161">Use el cable de Grove para conectar el sensor de temperatura Grove al puerto **A0** de Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="588e0-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Conectar al sensor de temperatura](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexión de Edison y el sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="588e0-164">Ahora el sensor está listo.</span><span class="sxs-lookup"><span data-stu-id="588e0-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="588e0-165">Encendido de Edison</span><span class="sxs-lookup"><span data-stu-id="588e0-165">Power up Edison</span></span>

1. <span data-ttu-id="588e0-166">Conecte la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="588e0-166">Plug in the power supply.</span></span>

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="588e0-168">Un LED verde (con la etiqueta DS1 en la placa de expansión de Arduino*) debería encenderse y permanecer encendido.</span><span class="sxs-lookup"><span data-stu-id="588e0-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="588e0-169">Espere un minuto para que termine de inicializarse la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="588e0-170">Si no tiene una fuente de alimentación de CC, puede encenderla usando un puerto USB.</span><span class="sxs-lookup"><span data-stu-id="588e0-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="588e0-171">Consulte la sección `Connect Edison to your computer` para más información.</span><span class="sxs-lookup"><span data-stu-id="588e0-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="588e0-172">La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.</span><span class="sxs-lookup"><span data-stu-id="588e0-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="588e0-173">Conexión de Edison a un equipo</span><span class="sxs-lookup"><span data-stu-id="588e0-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="588e0-174">Mueva hacia abajo el microconmutador (es decir, hacia los dos puertos microUSB) para activar el modo de dispositivo de Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="588e0-175">Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="588e0-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Desplazamiento hacia abajo del microconmutador](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="588e0-177">Conecte el cable microUSB al puerto microUSB superior.</span><span class="sxs-lookup"><span data-stu-id="588e0-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Puerto microUSB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="588e0-179">Conecte el otro extremo del cable USB al equipo.</span><span class="sxs-lookup"><span data-stu-id="588e0-179">Plug the other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="588e0-181">Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).</span><span class="sxs-lookup"><span data-stu-id="588e0-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="588e0-182">Descarga y ejecución de la herramienta de configuración</span><span class="sxs-lookup"><span data-stu-id="588e0-182">Download and run the configuration tool</span></span>
<span data-ttu-id="588e0-183">Obtenga la herramienta de configuración más reciente haciendo clic [aquí](https://software.intel.com/en-us/iot/hardware/edison/downloads) (los vínculos se encuentran bajo el título `Installers`).</span><span class="sxs-lookup"><span data-stu-id="588e0-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="588e0-184">Ejecute la herramienta y siga las instrucciones que aparecen en pantalla. Vaya haciendo clic en Next (Siguiente) según proceda.</span><span class="sxs-lookup"><span data-stu-id="588e0-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="588e0-185">Actualización del firmware</span><span class="sxs-lookup"><span data-stu-id="588e0-185">Flash firmware</span></span>
1. <span data-ttu-id="588e0-186">En la página `Set up options`, haga clic en `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="588e0-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="588e0-187">Seleccione la imagen que se instalará en la placa realizando una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="588e0-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="588e0-188">Para descargar e instalar en la placa la imagen del firmware más reciente de Intel, seleccione `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="588e0-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="588e0-189">Para actualizar el firmware de la placa con una imagen que ya ha guardado en el equipo, seleccione `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="588e0-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="588e0-190">Busque y seleccione la imagen con la que va a actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="588e0-191">La herramienta de instalación tratará de actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="588e0-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="588e0-192">La duración del proceso puede ser de hasta 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="588e0-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="588e0-193">Establecimiento de la contraseña</span><span class="sxs-lookup"><span data-stu-id="588e0-193">Set password</span></span>
1. <span data-ttu-id="588e0-194">En la página `Set up options`, haga clic en `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="588e0-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="588e0-195">Puede establecer un nombre personalizado para la placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="588e0-196">Esto es opcional.</span><span class="sxs-lookup"><span data-stu-id="588e0-196">This is optional.</span></span>
3. <span data-ttu-id="588e0-197">Escriba una contraseña para la placa y, luego, haga clic en `Set password`.</span><span class="sxs-lookup"><span data-stu-id="588e0-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="588e0-198">Anote la contraseña, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="588e0-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="588e0-199">Conexión a una red Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="588e0-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="588e0-200">En la página `Set up options`, haga clic en `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="588e0-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="588e0-201">Espere, como máximo, un minuto, ya que el equipo buscará las redes Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="588e0-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="588e0-202">En la lista desplegable `Detected Networks`, seleccione su red.</span><span class="sxs-lookup"><span data-stu-id="588e0-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="588e0-203">En la lista desplegable `Security`, seleccione el tipo de seguridad de la red.</span><span class="sxs-lookup"><span data-stu-id="588e0-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="588e0-204">Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="588e0-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="588e0-205">Anote la dirección IP, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="588e0-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="588e0-206">Asegúrese de que Edison se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="588e0-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="588e0-207">El equipo se conectará a Edison mediante la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="588e0-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Conectar al sensor de temperatura](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="588e0-209">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="588e0-209">Congratulations!</span></span> <span data-ttu-id="588e0-210">Ha configurado correctamente Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="588e0-211">Ejecutar una aplicación de ejemplo en Intel Edison</span><span class="sxs-lookup"><span data-stu-id="588e0-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="588e0-212">Preparar el SDK de dispositivo IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="588e0-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="588e0-213">Use uno de los siguientes clientes SSH del equipo host para conectar con Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="588e0-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="588e0-214">La dirección IP es la de la herramienta de configuración y la contraseña es la que ha establecido en esa herramienta.</span><span class="sxs-lookup"><span data-stu-id="588e0-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="588e0-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="588e0-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="588e0-216">El cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="588e0-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="588e0-217">Clone la aplicación cliente de ejemplo en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="588e0-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="588e0-218">Luego vaya a la carpeta de repositorio para ejecutar el comando siguiente a fin de instalar todos los paquetes, proceso que puede tardar varios minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="588e0-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-the-sample-application"></a><span data-ttu-id="588e0-219">Configurar y ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="588e0-219">Configure and run the sample application</span></span>

1. <span data-ttu-id="588e0-220">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="588e0-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="588e0-222">Hay dos macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="588e0-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="588e0-223">La primera es `INTERVAL`, que define el intervalo de tiempo entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="588e0-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="588e0-224">La segunda es `simulatedData`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="588e0-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="588e0-225">Si **no tiene el sensor**, establezca el valor `simulatedData` en `true` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="588e0-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="588e0-226">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="588e0-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="588e0-227">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="588e0-227">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="588e0-228">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="588e0-228">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="588e0-229">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Resultado: datos de sensor enviados desde Intel Edison a IoT Hub](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="588e0-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="588e0-231">Next steps</span></span>

<span data-ttu-id="588e0-232">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="588e0-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
