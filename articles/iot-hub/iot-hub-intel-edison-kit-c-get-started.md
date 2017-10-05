---
title: 'Intel Edison en la nube (C): Conectar Intel Edison a Azure IoT Hub | Microsoft Docs'
description: "Con este tutorial aprenderá a configurar y conectar Intel Edison a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: azure iot intel edison, intel edison iot hub, intel edison enviar datos a la nube, intel edison en la nube
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: edbdbe0230f742cd7228f04a4a83c9bd567527e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-c"></a><span data-ttu-id="6e26c-104">Conectar Intel Edison a Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="6e26c-104">Connect Intel Edison to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="6e26c-105">En este tutorial, empiece por aprender los conceptos básicos sobre cómo trabajar con Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="6e26c-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="6e26c-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="6e26c-107">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="6e26c-107">Don't have a kit yet?</span></span> <span data-ttu-id="6e26c-108">Comience [aquí](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="6e26c-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6e26c-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="6e26c-109">What you do</span></span>

* <span data-ttu-id="6e26c-110">Configure Intel Edison y los módulos de Grove.</span><span class="sxs-lookup"><span data-stu-id="6e26c-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="6e26c-111">Cree un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-111">Create an IoT hub.</span></span>
* <span data-ttu-id="6e26c-112">Registre un dispositivo para Edison en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="6e26c-113">Ejecute una aplicación de ejemplo en Edison para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="6e26c-114">Conecte Intel Edison al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="6e26c-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="6e26c-115">Luego ejecute una aplicación de ejemplo en Edison para recopilar datos de temperatura y humedad de un sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="6e26c-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="6e26c-116">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6e26c-117">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="6e26c-117">What you learn</span></span>

* <span data-ttu-id="6e26c-118">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="6e26c-119">Cómo conectar Edison a un sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="6e26c-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="6e26c-120">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="6e26c-121">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6e26c-122">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="6e26c-122">What you need</span></span>

![Lo que necesita](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="6e26c-124">La placa de Intel Edison</span><span class="sxs-lookup"><span data-stu-id="6e26c-124">The Intel Edison board</span></span>
* <span data-ttu-id="6e26c-125">La placa de expansión de Arduino.</span><span class="sxs-lookup"><span data-stu-id="6e26c-125">Arduino expansion board</span></span>
* <span data-ttu-id="6e26c-126">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-126">An active Azure subscription.</span></span> <span data-ttu-id="6e26c-127">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="6e26c-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="6e26c-128">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="6e26c-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="6e26c-129">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="6e26c-129">An Internet connection.</span></span>
* <span data-ttu-id="6e26c-130">Un cable USB Micro B a Tipo A.</span><span class="sxs-lookup"><span data-stu-id="6e26c-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="6e26c-131">Una fuente de alimentación de corriente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="6e26c-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="6e26c-132">La fuente de alimentación debe ser del siguiente tipo:</span><span class="sxs-lookup"><span data-stu-id="6e26c-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="6e26c-133">7-15 V CC.</span><span class="sxs-lookup"><span data-stu-id="6e26c-133">7-15V DC</span></span>
  - <span data-ttu-id="6e26c-134">Un mínimo de 1500 mA.</span><span class="sxs-lookup"><span data-stu-id="6e26c-134">At least 1500mA</span></span>
  - <span data-ttu-id="6e26c-135">La clavija central o interna debe ser el polo positivo de la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="6e26c-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="6e26c-136">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="6e26c-136">The following items are optional:</span></span>

* <span data-ttu-id="6e26c-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="6e26c-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="6e26c-138">Grove: sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="6e26c-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="6e26c-139">Cable de Grove</span><span class="sxs-lookup"><span data-stu-id="6e26c-139">Grove Cable</span></span>
* <span data-ttu-id="6e26c-140">Cualquiera de las piezas intermedias o los tornillos incluidos en el paquete, por ejemplo, los dos tornillos para fijar el módulo a la placa de expansión y los cuatro conjuntos de tornillos y separadores de plástico.</span><span class="sxs-lookup"><span data-stu-id="6e26c-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="6e26c-141">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="6e26c-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="6e26c-142">Configurar Intel Edison</span><span class="sxs-lookup"><span data-stu-id="6e26c-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="6e26c-143">Ensamblaje de la placa</span><span class="sxs-lookup"><span data-stu-id="6e26c-143">Assemble your board</span></span>

<span data-ttu-id="6e26c-144">En esta sección encontrará los pasos necesarios para conectar el módulo Intel® Edison a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="6e26c-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="6e26c-145">Coloque el módulo Intel® Edison dentro del contorno blanco de la placa de expansión, de forma que los agujeros del módulo queden alineados con los tornillos de la placa expansión.</span><span class="sxs-lookup"><span data-stu-id="6e26c-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="6e26c-146">Presione hacia abajo en el módulo, justo debajo de la frase `What will you make?`, hasta que oiga un chasquido.</span><span class="sxs-lookup"><span data-stu-id="6e26c-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="6e26c-148">Utilice las dos tuercas hexagonales (incluidas en el paquete) para fijar el módulo a la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="6e26c-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="6e26c-150">Inserte un tornillo en uno de los cuatro agujeros de las esquinas de la placa de expansión.</span><span class="sxs-lookup"><span data-stu-id="6e26c-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="6e26c-151">Gire y apriete uno de los separadores de plástico blancos sobre el tornillo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="6e26c-153">Repita el paso anterior con los otros tres separadores de las esquinas.</span><span class="sxs-lookup"><span data-stu-id="6e26c-153">Repeat for the other three corner spacers.</span></span>

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="6e26c-155">Ya ha ensamblado la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-155">Now your board is assembled.</span></span>

   ![Placa ensamblada](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="6e26c-157">Conectar Grove Base Shield y el sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="6e26c-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="6e26c-158">Coloque Grove Base Shield en la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="6e26c-159">Asegúrese de que todas las patillas estén bien conectadas a la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="6e26c-161">Use el cable de Grove para conectar el sensor de temperatura Grove al puerto **A0** de Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="6e26c-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Conectar al sensor de temperatura](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Conexión de Edison y el sensor](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="6e26c-164">Ahora el sensor está listo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="6e26c-165">Encendido de Edison</span><span class="sxs-lookup"><span data-stu-id="6e26c-165">Power up Edison</span></span>

1. <span data-ttu-id="6e26c-166">Conecte la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="6e26c-166">Plug in the power supply.</span></span>

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="6e26c-168">Un LED verde (con la etiqueta DS1 en la placa de expansión de Arduino*) debería encenderse y permanecer encendido.</span><span class="sxs-lookup"><span data-stu-id="6e26c-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="6e26c-169">Espere un minuto para que termine de inicializarse la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e26c-170">Si no tiene una fuente de alimentación de CC, puede encenderla usando un puerto USB.</span><span class="sxs-lookup"><span data-stu-id="6e26c-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="6e26c-171">Consulte la sección `Connect Edison to your computer` para más información.</span><span class="sxs-lookup"><span data-stu-id="6e26c-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="6e26c-172">La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.</span><span class="sxs-lookup"><span data-stu-id="6e26c-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="6e26c-173">Conexión de Edison a un equipo</span><span class="sxs-lookup"><span data-stu-id="6e26c-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="6e26c-174">Mueva hacia abajo el microconmutador (es decir, hacia los dos puertos microUSB) para activar el modo de dispositivo de Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="6e26c-175">Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="6e26c-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Desplazamiento hacia abajo del microconmutador](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="6e26c-177">Conecte el cable microUSB al puerto microUSB superior.</span><span class="sxs-lookup"><span data-stu-id="6e26c-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Puerto microUSB superior](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="6e26c-179">Conecte el otro extremo del cable USB al equipo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-179">Plug the other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="6e26c-181">Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).</span><span class="sxs-lookup"><span data-stu-id="6e26c-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="6e26c-182">Descarga y ejecución de la herramienta de configuración</span><span class="sxs-lookup"><span data-stu-id="6e26c-182">Download and run the configuration tool</span></span>
<span data-ttu-id="6e26c-183">Obtenga la herramienta de configuración más reciente haciendo clic [aquí](https://software.intel.com/en-us/iot/hardware/edison/downloads) (los vínculos se encuentran bajo el título `Installers`).</span><span class="sxs-lookup"><span data-stu-id="6e26c-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="6e26c-184">Ejecute la herramienta y siga las instrucciones que aparecen en pantalla. Vaya haciendo clic en Next (Siguiente) según proceda.</span><span class="sxs-lookup"><span data-stu-id="6e26c-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="6e26c-185">Actualización del firmware</span><span class="sxs-lookup"><span data-stu-id="6e26c-185">Flash firmware</span></span>
1. <span data-ttu-id="6e26c-186">En la página `Set up options`, haga clic en `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="6e26c-187">Seleccione la imagen que se instalará en la placa realizando una de las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="6e26c-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="6e26c-188">Para descargar e instalar en la placa la imagen del firmware más reciente de Intel, seleccione `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="6e26c-189">Para actualizar el firmware de la placa con una imagen que ya ha guardado en el equipo, seleccione `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="6e26c-190">Busque y seleccione la imagen con la que va a actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="6e26c-191">La herramienta de instalación tratará de actualizar el firmware de la placa.</span><span class="sxs-lookup"><span data-stu-id="6e26c-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="6e26c-192">La duración del proceso puede ser de hasta 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="6e26c-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="6e26c-193">Establecimiento de la contraseña</span><span class="sxs-lookup"><span data-stu-id="6e26c-193">Set password</span></span>
1. <span data-ttu-id="6e26c-194">En la página `Set up options`, haga clic en `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="6e26c-195">Puede establecer un nombre personalizado para la placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="6e26c-196">Esto es opcional.</span><span class="sxs-lookup"><span data-stu-id="6e26c-196">This is optional.</span></span>
3. <span data-ttu-id="6e26c-197">Escriba una contraseña para la placa y, luego, haga clic en `Set password`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="6e26c-198">Anote la contraseña, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="6e26c-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="6e26c-199">Conexión a una red Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="6e26c-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="6e26c-200">En la página `Set up options`, haga clic en `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="6e26c-201">Espere, como máximo, un minuto, ya que el equipo buscará las redes Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="6e26c-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="6e26c-202">En la lista desplegable `Detected Networks`, seleccione su red.</span><span class="sxs-lookup"><span data-stu-id="6e26c-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="6e26c-203">En la lista desplegable `Security`, seleccione el tipo de seguridad de la red.</span><span class="sxs-lookup"><span data-stu-id="6e26c-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="6e26c-204">Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="6e26c-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="6e26c-205">Anote la dirección IP, ya que la usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="6e26c-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="6e26c-206">Asegúrese de que Edison se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="6e26c-207">El equipo se conectará a Edison mediante la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="6e26c-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Conectar al sensor de temperatura](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="6e26c-209">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="6e26c-209">Congratulations!</span></span> <span data-ttu-id="6e26c-210">Ha configurado correctamente Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="6e26c-211">Ejecutar una aplicación de ejemplo en Intel Edison</span><span class="sxs-lookup"><span data-stu-id="6e26c-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="6e26c-212">Preparar el SDK de dispositivo IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="6e26c-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="6e26c-213">Use uno de los siguientes clientes SSH del equipo host para conectar con Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="6e26c-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="6e26c-214">La dirección IP es la de la herramienta de configuración y la contraseña es la que ha establecido en esa herramienta.</span><span class="sxs-lookup"><span data-stu-id="6e26c-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="6e26c-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="6e26c-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="6e26c-216">El cliente de SSH integrado en Ubuntu o macOS (ejecute `ssh root@"the IP address"`).</span><span class="sxs-lookup"><span data-stu-id="6e26c-216">The built-in SSH client on Ubuntu or macOS (run `ssh root@"the IP address"`).</span></span>

2. <span data-ttu-id="6e26c-217">Clone la aplicación cliente de ejemplo en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6e26c-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="6e26c-218">Luego vaya a la carpeta de repositorio para ejecutar el comando siguiente a fin de compilar el SDK IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e26c-218">Then navigate to the repo folder to run the following command to build Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-the-sample-application"></a><span data-ttu-id="6e26c-219">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6e26c-219">Configure the sample application</span></span>

1. <span data-ttu-id="6e26c-220">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6e26c-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Archivo config](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="6e26c-222">Hay dos macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="6e26c-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="6e26c-223">La primera es `INTERVAL`, que define el intervalo de tiempo entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="6e26c-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="6e26c-224">La segunda es `SIMULATED_DATA`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="6e26c-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="6e26c-225">Si **no tiene el sensor**, establezca el valor `SIMULATED_DATA` en `1` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="6e26c-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="6e26c-226">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="6e26c-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="6e26c-227">Compilar y ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6e26c-227">Build and run the sample application</span></span>

1. <span data-ttu-id="6e26c-228">Compile la aplicación de ejemplo al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="6e26c-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Resultado de la compilación](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="6e26c-230">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="6e26c-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="6e26c-231">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="6e26c-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="6e26c-232">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Resultado: datos de sensor enviados desde Intel Edison a IoT Hub](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="6e26c-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e26c-234">Next steps</span></span>

<span data-ttu-id="6e26c-235">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="6e26c-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
