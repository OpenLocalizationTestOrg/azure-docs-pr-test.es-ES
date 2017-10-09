---
title: aaaIntel Edison toocloud (Node.js) - conectar Intel Edison tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse Intel Edison tooAzure centro de IoT para la plataforma de nube de Azure de Intel Edison toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel centro de iot edison, intel edison enviar datos toocloud, intel edison toocloud
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="e9a7b-104">Conectar Intel Edison tooAzure centro de IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="e9a7b-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="e9a7b-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con Edison de Intel.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="e9a7b-106">A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e9a7b-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="e9a7b-107">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="e9a7b-107">Don't have a kit yet?</span></span> <span data-ttu-id="e9a7b-108">Comience [aquí](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="e9a7b-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="e9a7b-109">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="e9a7b-109">What you do</span></span>

* <span data-ttu-id="e9a7b-110">Configure Intel Edison y los módulos de Grove.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="e9a7b-111">Cree un IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-111">Create an IoT hub.</span></span>
* <span data-ttu-id="e9a7b-112">Registre un dispositivo para Edison en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="e9a7b-113">Ejecutar una aplicación de ejemplo en el centro de IoT Edison toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="e9a7b-114">Conectar el centro de IoT de tooan Edison de Intel que cree.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="e9a7b-115">A continuación, ejecutar una aplicación de ejemplo en Edison toocollect temperatura y humedad datos de un sensor de temperatura de arboleda.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="e9a7b-116">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="e9a7b-117">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="e9a7b-117">What you learn</span></span>

* <span data-ttu-id="e9a7b-118">¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="e9a7b-119">¿Cómo tooconnect Edison con un sensor de temperatura de arboleda.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="e9a7b-120">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en Edison.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="e9a7b-121">Cómo centro de IoT de toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e9a7b-122">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="e9a7b-122">What you need</span></span>

![Lo que necesita](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="e9a7b-124">Hola panel Edison de Intel</span><span class="sxs-lookup"><span data-stu-id="e9a7b-124">hello Intel Edison board</span></span>
* <span data-ttu-id="e9a7b-125">La placa de expansión de Arduino.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-125">Arduino expansion board</span></span>
* <span data-ttu-id="e9a7b-126">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-126">An active Azure subscription.</span></span> <span data-ttu-id="e9a7b-127">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="e9a7b-128">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="e9a7b-129">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-129">An Internet connection.</span></span>
* <span data-ttu-id="e9a7b-130">Un cable USB A tooType de Micro B</span><span class="sxs-lookup"><span data-stu-id="e9a7b-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="e9a7b-131">Una fuente de alimentación de corriente continua (CC).</span><span class="sxs-lookup"><span data-stu-id="e9a7b-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="e9a7b-132">La fuente de alimentación debe ser del siguiente tipo:</span><span class="sxs-lookup"><span data-stu-id="e9a7b-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="e9a7b-133">7-15 V CC.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-133">7-15V DC</span></span>
  - <span data-ttu-id="e9a7b-134">Un mínimo de 1500 mA.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-134">At least 1500mA</span></span>
  - <span data-ttu-id="e9a7b-135">pin de Hello center o interna debe ser polo positivo de Hola Hola de fuente de alimentación</span><span class="sxs-lookup"><span data-stu-id="e9a7b-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="e9a7b-136">Hola siguientes elementos es opcional:</span><span class="sxs-lookup"><span data-stu-id="e9a7b-136">hello following items are optional:</span></span>

* <span data-ttu-id="e9a7b-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="e9a7b-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="e9a7b-138">Grove: sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="e9a7b-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="e9a7b-139">Cable de Grove</span><span class="sxs-lookup"><span data-stu-id="e9a7b-139">Grove Cable</span></span>
* <span data-ttu-id="e9a7b-140">Las barras de separación o tornillos incluidos en el empaquetado de hello, incluida la tarjeta de expansión de dos tornillos toofasten Hola módulo toohello y cuatro conjuntos de tornillos y separadores de plástico.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="e9a7b-141">Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="e9a7b-142">Configurar Intel Edison</span><span class="sxs-lookup"><span data-stu-id="e9a7b-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="e9a7b-143">Ensamblaje de la placa</span><span class="sxs-lookup"><span data-stu-id="e9a7b-143">Assemble your board</span></span>

<span data-ttu-id="e9a7b-144">Esta sección contiene pasos tooattach su tarjeta de expansión de Intel® Edison módulo tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="e9a7b-145">Coloque el módulo de Intel® Edison de hello en esquema Hola blanco en su tarjeta de expansión, se alinea vulnerabilidades de hello en el módulo de hello con tornillos de hello en la tarjeta de expansión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="e9a7b-146">Mantenga presionada en módulo de hello justo debajo de palabras de hello `What will you make?` hasta que cree un complemento.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Ensamblado de la placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="e9a7b-148">Utilice Hola dos frutos hexadecimal (incluidos en el paquete de hello) toosecure Hola módulo toohello expansión placa.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Ensamblado de la placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="e9a7b-150">Inserte un tornillo en uno de cuatro agujeros de esquina hello en la tarjeta de expansión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="e9a7b-151">Retorcer y apriete uno de los separadores de plástico blanco hello en tornillo Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Ensamblado de la placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="e9a7b-153">Repita este paso para Hola otros separadores de esquina de tres.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-153">Repeat for hello other three corner spacers.</span></span>

   ![Ensamblado de la placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="e9a7b-155">Ya ha ensamblado la placa.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-155">Now your board is assembled.</span></span>

   ![Placa ensamblada](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="e9a7b-157">Conectar hello arboleda Base escudo y sensor de temperatura de Hola</span><span class="sxs-lookup"><span data-stu-id="e9a7b-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="e9a7b-158">Coloque hello arboleda Base escudo en panel de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="e9a7b-159">Asegúrese de que todas las patillas estén bien conectadas a la placa.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="e9a7b-161">Sensor de temperatura de uso arboleda Cable tooconnect arboleda en hello escudo de Base de arboleda **A0** puerto.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Conecte sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexión de Edison y el sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="e9a7b-164">Ahora el sensor está listo.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="e9a7b-165">Encendido de Edison</span><span class="sxs-lookup"><span data-stu-id="e9a7b-165">Power up Edison</span></span>

1. <span data-ttu-id="e9a7b-166">Conecte en fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-166">Plug in hello power supply.</span></span>

   ![Conexión de la fuente de alimentación](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="e9a7b-168">Un LED verde (con la etiqueta DS1 en hello tarjeta de expansión Arduino *) debe encenderse y permanecer encendido.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="e9a7b-169">Espere un minuto para hello panel toofinish arrancado.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e9a7b-170">Si no tiene una fuente de alimentación de controlador de dominio, puede placa de Hola de alimentación a través de un puerto USB.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="e9a7b-171">Consulte la sección `Connect Edison tooyour computer` para más información.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="e9a7b-172">La placa puede presentar un comportamiento imprevisible si se enciende de este modo, especialmente cuando se utilizan redes Wi-Fi o motores de accionamiento.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="e9a7b-173">Conectar Edison tooyour equipo</span><span class="sxs-lookup"><span data-stu-id="e9a7b-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="e9a7b-174">Alternar hacia abajo Hola microconmutador hacia Hola dos micro puertos USB para que Edison está en modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="e9a7b-175">Para ver las diferencias entre los modos host y dispositivo, consulte [esta página](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="e9a7b-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Alternar hacia abajo microconmutador Hola](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="e9a7b-177">Enchufe cable USB micro de hello en puerto USB de micro superior Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Puerto microUSB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="e9a7b-179">Plug Hola otro extremo del cable USB en el equipo.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Cable USB conectado a un equipo](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="e9a7b-181">Sabrá que la placa se ha terminado de inicializar cuando en el equipo aparezca una unidad nueva (es muy parecido a cuando se inserta una tarjeta SD en el equipo).</span><span class="sxs-lookup"><span data-stu-id="e9a7b-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="e9a7b-182">Descargue y ejecute la herramienta de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="e9a7b-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="e9a7b-183">Obtener la herramienta de configuración más reciente de Hola de [este vínculo](https://software.intel.com/en-us/iot/hardware/edison/downloads) aparecen en hello `Installers` encabezado.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="e9a7b-184">Ejecutar la herramienta de Hola y siga su pantalla instrucciones, hacer clic en siguiente cuando sea necesario</span><span class="sxs-lookup"><span data-stu-id="e9a7b-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="e9a7b-185">Actualización del firmware</span><span class="sxs-lookup"><span data-stu-id="e9a7b-185">Flash firmware</span></span>
1. <span data-ttu-id="e9a7b-186">En hello `Set up options` página, haga clic en `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="e9a7b-187">Seleccione tooflash de imagen de hello en el panel, realice uno de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="e9a7b-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="e9a7b-188">toodownload y flash, seleccione el panel con la imagen de firmware más reciente de hello disponible de Intel, `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="e9a7b-189">Seleccione el panel con una imagen que ya se ha guardado en el equipo de tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="e9a7b-190">Busque la imagen de hello seleccione tooand desea tooflash tooyour panel.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="e9a7b-191">herramienta de configuración de Hello intentará tooflash el panel.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="e9a7b-192">todo el proceso intermitente Hola puede tardar minutos too10.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="e9a7b-193">Establecimiento de la contraseña</span><span class="sxs-lookup"><span data-stu-id="e9a7b-193">Set password</span></span>
1. <span data-ttu-id="e9a7b-194">En hello `Set up options` página, haga clic en `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="e9a7b-195">Puede establecer un nombre personalizado para la placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="e9a7b-196">Esto es opcional.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-196">This is optional.</span></span>
3. <span data-ttu-id="e9a7b-197">Escriba una contraseña para la placa y, luego, haga clic en `Set password`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="e9a7b-198">Marcar como inactiva la contraseña de hello, que se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="e9a7b-199">Conexión a una red Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="e9a7b-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="e9a7b-200">En hello `Set up options` página, haga clic en `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="e9a7b-201">Espera tooone minuto como los análisis del equipo para las redes Wi-Fi disponibles.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="e9a7b-202">De hello `Detected Networks` lista desplegable, seleccione la red.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="e9a7b-203">De hello `Security` lista desplegable, tipo de seguridad de la red de hello select.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="e9a7b-204">Proporcione los datos de inicio de sesión y contraseña. Después, haga clic en `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="e9a7b-205">Marcar como inactiva Hola dirección IP, que se utiliza más adelante.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="e9a7b-206">Asegúrese de que ese Edison está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="e9a7b-207">El equipo conecta tooyour Edison utilizando la dirección IP de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Conecte sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="e9a7b-209">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="e9a7b-209">Congratulations!</span></span> <span data-ttu-id="e9a7b-210">Ha configurado correctamente Edison.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="e9a7b-211">Ejecutar una aplicación de ejemplo en Intel Edison</span><span class="sxs-lookup"><span data-stu-id="e9a7b-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="e9a7b-212">Preparar Hola SDK de dispositivos de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="e9a7b-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="e9a7b-213">Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host Edison de Intel.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="e9a7b-214">dirección IP de Hello procede de la herramienta de configuración de Hola y contraseña de hello es Hola uno que haya establecido en esa herramienta.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="e9a7b-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="e9a7b-216">cliente SSH integrado de Hello en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="e9a7b-217">Dispositivo de tooyour de la aplicación de cliente de ejemplo con clonación Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="e9a7b-218">A continuación, navegue Hola de toorun de carpeta toohello repositorio después comando tooinstall todos los paquetes, puede tardar serval minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="e9a7b-219">Configurar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="e9a7b-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="e9a7b-220">Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="e9a7b-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="e9a7b-222">Hay dos macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="e9a7b-223">Hello primero uno es `INTERVAL`, que define el intervalo de tiempo de hello entre dos mensajes que envían toocloud.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="e9a7b-224">Hola otra `simulatedData`, que es un valor booleano para si toouse simulado los datos de sensor o no.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="e9a7b-225">Si se **no tiene el sensor de hello**, hello establezca `simulatedData` valor demasiado`true` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="e9a7b-226">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="e9a7b-227">Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e9a7b-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="e9a7b-228">Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="e9a7b-229">Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Salida: datos de sensor enviados desde el centro de IoT de Intel Edison tooyour](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="e9a7b-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e9a7b-231">Next steps</span></span>

<span data-ttu-id="e9a7b-232">Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="e9a7b-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
