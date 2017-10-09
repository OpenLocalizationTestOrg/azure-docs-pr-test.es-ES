---
title: aaaRaspberry Pi toocloud (Node.js) - conectar frambuesa Pi tooAzure centro de IoT | Documentos de Microsoft
description: Conectar frambuesa Pi tooAzure centro de IoT de frambuesa Pi toosend datos toohello nube de Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Azure iot frambuesas pi, frambuesas pi iot hub, frambuesas pi envío datos toocloud, frambuesas pi toocloud"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="c70c3-104">Conectar frambuesa Pi tooAzure centro de IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="c70c3-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="c70c3-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con frambuesa Pi que se está ejecutando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c70c3-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="c70c3-106">A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="c70c3-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="c70c3-107">Para obtener ejemplos de Windows 10 IoT Core, vaya toohello [centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="c70c3-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="c70c3-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="c70c3-108">Don't have a kit yet?</span></span> <span data-ttu-id="c70c3-109">Intente hello [frambuesa Pi 3 emulador](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="c70c3-109">Try hello [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="c70c3-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="c70c3-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c70c3-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="c70c3-111">What you do</span></span>

* <span data-ttu-id="c70c3-112">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="c70c3-113">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c70c3-113">Create an IoT hub.</span></span>
* <span data-ttu-id="c70c3-114">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c70c3-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="c70c3-115">Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="c70c3-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="c70c3-116">Conectar el centro de IoT de frambuesa Pi tooan creados por usted.</span><span class="sxs-lookup"><span data-stu-id="c70c3-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="c70c3-117">A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect Pi de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="c70c3-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="c70c3-118">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="c70c3-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="c70c3-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="c70c3-119">What you learn</span></span>

* <span data-ttu-id="c70c3-120">¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c70c3-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="c70c3-121">¿Cómo tooconnect Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="c70c3-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="c70c3-122">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo de Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="c70c3-123">Cómo centro de IoT de toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="c70c3-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c70c3-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c70c3-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="c70c3-126">Hola frambuesa Pi 2 o 3 de Pi de frambuesa al panel.</span><span class="sxs-lookup"><span data-stu-id="c70c3-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="c70c3-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c70c3-127">An active Azure subscription.</span></span> <span data-ttu-id="c70c3-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c70c3-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="c70c3-129">Un monitor, un teclado USB y mouse (ratón) que se conectan tooPi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="c70c3-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="c70c3-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="c70c3-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="c70c3-131">An Internet connection.</span></span>
* <span data-ttu-id="c70c3-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="c70c3-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="c70c3-133">Un SD USB adaptador o microSD tarjeta tooburn Hola imagen de sistema operativo en tarjeta microSD de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="c70c3-134">Alimentación de amp 2 de 5 voltios con cable de hello pie 6 micro USB.</span><span class="sxs-lookup"><span data-stu-id="c70c3-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="c70c3-135">Hola siguientes elementos es opcional:</span><span class="sxs-lookup"><span data-stu-id="c70c3-135">hello following items are optional:</span></span>

* <span data-ttu-id="c70c3-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="c70c3-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="c70c3-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="c70c3-137">A breadboard.</span></span>
* <span data-ttu-id="c70c3-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="c70c3-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="c70c3-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="c70c3-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="c70c3-140">Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="c70c3-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="c70c3-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="c70c3-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="c70c3-142">Instalar el sistema operativo de hello Raspbian de Pi</span><span class="sxs-lookup"><span data-stu-id="c70c3-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="c70c3-143">Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="c70c3-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="c70c3-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="c70c3-145">[Descargar Raspbian Jessie con píxeles](https://www.raspberrypi.org/downloads/raspbian/) (archivo .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="c70c3-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="c70c3-146">Extraer hello Raspbian imagen tooa carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="c70c3-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="c70c3-147">Instalar Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c70c3-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="c70c3-148">[Descargar e instalar la utilidad de grabadora de tarjeta de SD de creación de hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="c70c3-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="c70c3-149">Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="c70c3-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="c70c3-150">Seleccione la unidad de tarjeta microSD Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-150">Select hello microSD card drive.</span></span> <span data-ttu-id="c70c3-151">Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="c70c3-152">Haga clic en Flash tooinstall Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="c70c3-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="c70c3-153">Quitar tarjeta microSD de hello del equipo cuando se completa la instalación.</span><span class="sxs-lookup"><span data-stu-id="c70c3-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="c70c3-154">Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.</span><span class="sxs-lookup"><span data-stu-id="c70c3-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="c70c3-155">Inserte la tarjeta microSD de hello en Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="c70c3-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="c70c3-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="c70c3-157">Conecte el monitor de toohello de Pi, teclado y mouse (ratón), inicie Pi y, a continuación, inicie sesión en Raspbian con `pi` como nombre de usuario de Hola y `raspberry` como contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="c70c3-158">Haga clic en icono frambuesas hello > **preferencias** > **frambuesa Pi configuración**.</span><span class="sxs-lookup"><span data-stu-id="c70c3-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menú de Hello Raspbian preferencias](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="c70c3-160">En hello **Interfaces** pestaña, establezca **I2C** y **SSH** demasiado**habilitar**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c70c3-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="c70c3-161">Si no tiene sensores físicos y desea que los datos de sensor toouse simulado, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="c70c3-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="c70c3-163">tooenable SSH y I2C, puede encontrar varios documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="c70c3-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="c70c3-164">Conectar Hola sensor tooPi</span><span class="sxs-lookup"><span data-stu-id="c70c3-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="c70c3-165">Utilice hello breadboard y puentes cables tooconnect un LED y un tooPi BME280 como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="c70c3-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="c70c3-166">Si no dispone de sensor hello, omita esta sección.</span><span class="sxs-lookup"><span data-stu-id="c70c3-166">If you don’t have hello sensor, skip this section.</span></span>

![Hola frambuesa Pi y sensor de conexión](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="c70c3-168">sensor de Hello BME280 puede recopilar datos de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="c70c3-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="c70c3-169">Y Hola LED parpadea si se produce una comunicación entre el dispositivo y hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="c70c3-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="c70c3-170">Para el PIN de sensor, use Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="c70c3-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="c70c3-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="c70c3-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="c70c3-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="c70c3-172">End (Board)</span></span>            | <span data-ttu-id="c70c3-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="c70c3-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="c70c3-174">VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="c70c3-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="c70c3-175">Potencia 3,3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="c70c3-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="c70c3-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="c70c3-176">White cable</span></span>   |
| <span data-ttu-id="c70c3-177">GND (patilla 7G)</span><span class="sxs-lookup"><span data-stu-id="c70c3-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="c70c3-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="c70c3-178">GND (Pin 6)</span></span>            | <span data-ttu-id="c70c3-179">Cable marrón</span><span class="sxs-lookup"><span data-stu-id="c70c3-179">Brown cable</span></span>   |
| <span data-ttu-id="c70c3-180">SCK (patilla 8G)</span><span class="sxs-lookup"><span data-stu-id="c70c3-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="c70c3-181">I2C1 SDA (patilla 3)</span><span class="sxs-lookup"><span data-stu-id="c70c3-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="c70c3-182">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="c70c3-182">Orange cable</span></span>  |
| <span data-ttu-id="c70c3-183">SDI (patilla 10G)</span><span class="sxs-lookup"><span data-stu-id="c70c3-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="c70c3-184">I2C1 SCL (patilla 5)</span><span class="sxs-lookup"><span data-stu-id="c70c3-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="c70c3-185">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="c70c3-185">Red cable</span></span>     |
| <span data-ttu-id="c70c3-186">LED VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="c70c3-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="c70c3-187">GPIO 24 (patilla 18)</span><span class="sxs-lookup"><span data-stu-id="c70c3-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="c70c3-188">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="c70c3-188">White cable</span></span>   |
| <span data-ttu-id="c70c3-189">LED GND (patilla 17F)</span><span class="sxs-lookup"><span data-stu-id="c70c3-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="c70c3-190">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="c70c3-190">GND (Pin 20)</span></span>           | <span data-ttu-id="c70c3-191">Cable negro</span><span class="sxs-lookup"><span data-stu-id="c70c3-191">Black cable</span></span>   |

<span data-ttu-id="c70c3-192">Haga clic en tooview [frambuesa Pi 2 y 3 asignaciones de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="c70c3-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="c70c3-193">Una vez se haya conectado correctamente BME280 tooyour frambuesa Pi, debería ser como debajo de imagen.</span><span class="sxs-lookup"><span data-stu-id="c70c3-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="c70c3-195">Conectar red toohello de Pi</span><span class="sxs-lookup"><span data-stu-id="c70c3-195">Connect Pi toohello network</span></span>

<span data-ttu-id="c70c3-196">Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="c70c3-197">Use Hola Ethernet por cable tooconnect Pi tooyour con cable de red o siga hello [las instrucciones de hello frambuesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) red inalámbrica de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="c70c3-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="c70c3-198">Después de que el instalador de plataforma ha sido red toohello conectado correctamente, deberá tootake una nota de hello [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="c70c3-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Red toowired conectado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="c70c3-200">Asegúrese de que ese Pi está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="c70c3-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="c70c3-201">Por ejemplo, si el equipo está conectado tooa red inalámbrica mientras Pi es tooa conectado por cable de red, no verá Hola IP dirección en la salida de hello devdisco.</span><span class="sxs-lookup"><span data-stu-id="c70c3-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="c70c3-202">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="c70c3-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="c70c3-203">Clonar aplicación de ejemplo e instalar paquetes de requisitos previos de Hola</span><span class="sxs-lookup"><span data-stu-id="c70c3-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="c70c3-204">Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
    - <span data-ttu-id="c70c3-205">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="c70c3-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="c70c3-206">Necesitará Hola dirección IP de su tooconnect Pi esta a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="c70c3-206">You need hello IP address of your Pi tooconnect it via SSH.</span></span>
    - <span data-ttu-id="c70c3-207">cliente SSH integrado de Hello en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="c70c3-207">hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="c70c3-208">Debe ejecutar `ssh pi@<ip address of pi>` tooconnect Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="c70c3-208">You might need run `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="c70c3-209">el nombre de usuario de Hello predeterminada es `pi` , y es la contraseña de hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="c70c3-209">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="c70c3-210">Instalar Node.js y NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-210">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="c70c3-211">Primero debe comprobar la versión de Node.js con el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-211">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="c70c3-212">Si la versión de hello es inferior a 4.x o no hay ningún Node.js en el Pi, a continuación, ejecute hello después tooinstall de comando o actualizar Node.js.</span><span class="sxs-lookup"><span data-stu-id="c70c3-212">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="c70c3-213">Clonar aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c70c3-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="c70c3-214">Instale todos los paquetes mediante el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-214">Install all packages by hello following command.</span></span> <span data-ttu-id="c70c3-215">Incluye el SDK de dispositivo IoT de Azure, la biblioteca del sensor BME280 y la biblioteca de cableado de Pi.</span><span class="sxs-lookup"><span data-stu-id="c70c3-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="c70c3-216">Es posible que tarde varios toofinish minutos este denpening del proceso de instalación en la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="c70c3-216">It might take several minutes toofinish this installation process denpening on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="c70c3-217">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="c70c3-217">Configure hello sample application</span></span>

1. <span data-ttu-id="c70c3-218">Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c70c3-218">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="c70c3-220">Hay dos elementos en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="c70c3-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="c70c3-221">Hello primero uno es `interval`, que define el intervalo de tiempo de hello entre dos mensajes que envían toocloud.</span><span class="sxs-lookup"><span data-stu-id="c70c3-221">hello first one is `interval`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="c70c3-222">Hola otra `simulatedData`, que es un valor booleano para si toouse simulado los datos de sensor o no.</span><span class="sxs-lookup"><span data-stu-id="c70c3-222">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="c70c3-223">Si se **no tiene el sensor de hello**, hello establezca `simulatedData` valor demasiado`true` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.</span><span class="sxs-lookup"><span data-stu-id="c70c3-223">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="c70c3-224">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="c70c3-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="c70c3-225">Ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="c70c3-225">Run hello sample application</span></span>

1. <span data-ttu-id="c70c3-226">Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c70c3-226">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="c70c3-227">Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.</span><span class="sxs-lookup"><span data-stu-id="c70c3-227">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="c70c3-228">Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c70c3-228">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="c70c3-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c70c3-230">Next steps</span></span>

<span data-ttu-id="c70c3-231">Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c70c3-231">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]