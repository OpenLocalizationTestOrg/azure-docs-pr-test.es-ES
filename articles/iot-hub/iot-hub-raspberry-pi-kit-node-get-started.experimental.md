---
title: 'Raspberry Pi a la nube (Node.js): Conectar Raspberry Pi a Azure IoT Hub | Microsoft Docs'
description: "Conecte Raspberry Pi a Azure IoT Hub para que Raspberry Pi envíe datos a la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envía datos a la nube, raspberry pi a la nube"
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
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="165a3-104">Conectar Raspberry Pi a Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="165a3-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="165a3-105">En este tutorial, empezará por aprender los principios básicos del uso de Raspberry Pi que ejecuta Raspbian.</span><span class="sxs-lookup"><span data-stu-id="165a3-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="165a3-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="165a3-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="165a3-107">Para obtener ejemplos de Windows 10 IoT Core, vaya al [Centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="165a3-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="165a3-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="165a3-108">Don't have a kit yet?</span></span> <span data-ttu-id="165a3-109">Pruebe el [emulador de Raspberry Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="165a3-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="165a3-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="165a3-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="165a3-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="165a3-111">What you do</span></span>

* <span data-ttu-id="165a3-112">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="165a3-113">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="165a3-113">Create an IoT hub.</span></span>
* <span data-ttu-id="165a3-114">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="165a3-115">Ejecute una aplicación de ejemplo en Pi para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="165a3-116">Conecte Raspberry Pi al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="165a3-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="165a3-117">Luego ejecute una aplicación de ejemplo en Pi para recopilar datos de temperatura y humedad de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="165a3-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="165a3-118">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="165a3-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="165a3-119">What you learn</span></span>

* <span data-ttu-id="165a3-120">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="165a3-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="165a3-121">Cómo conectar Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="165a3-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="165a3-122">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="165a3-123">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="165a3-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="165a3-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="165a3-126">La placa de Raspberry Pi 2 o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="165a3-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="165a3-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="165a3-127">An active Azure subscription.</span></span> <span data-ttu-id="165a3-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="165a3-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="165a3-129">Un monitor, un teclado USB y un mouse que se conecten a Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="165a3-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="165a3-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="165a3-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="165a3-131">An Internet connection.</span></span>
* <span data-ttu-id="165a3-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="165a3-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="165a3-133">Un adaptador de USB a SD o una tarjeta microSD para grabar la imagen del sistema operativo en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="165a3-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="165a3-134">Una fuente de alimentación de 5 V y 2 A con un cable microUSB de 6 pies.</span><span class="sxs-lookup"><span data-stu-id="165a3-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="165a3-135">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="165a3-135">The following items are optional:</span></span>

* <span data-ttu-id="165a3-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="165a3-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="165a3-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="165a3-137">A breadboard.</span></span>
* <span data-ttu-id="165a3-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="165a3-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="165a3-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="165a3-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="165a3-140">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="165a3-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="165a3-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="165a3-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="165a3-142">Instalar el sistema operativo Raspbian para Pi</span><span class="sxs-lookup"><span data-stu-id="165a3-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="165a3-143">Prepare la tarjeta microSD para instalar la imagen de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="165a3-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="165a3-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="165a3-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="165a3-145">[Descargue Raspbian Jessie con Pixel](https://www.raspberrypi.org/downloads/raspbian/) (el archivo .zip).</span><span class="sxs-lookup"><span data-stu-id="165a3-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="165a3-146">Extraiga la imagen de Raspbian en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="165a3-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="165a3-147">Instale Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="165a3-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="165a3-148">[Descargue e instale la utilidad de grabadora de tarjetas SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="165a3-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="165a3-149">Ejecute Etcher y seleccione la imagen de Raspbian que extrajo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="165a3-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="165a3-150">Seleccione la unidad de la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="165a3-150">Select the microSD card drive.</span></span> <span data-ttu-id="165a3-151">Tenga en cuenta que es posible que Etcher ya haya seleccionado la unidad correcta.</span><span class="sxs-lookup"><span data-stu-id="165a3-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="165a3-152">Haga clic en Flash para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="165a3-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="165a3-153">Quite la tarjeta microSD del equipo cuando se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="165a3-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="165a3-154">Es seguro quitar la tarjeta microSD directamente porque Etcher expulsa o desmonta la tarjeta microSD automáticamente al acabar.</span><span class="sxs-lookup"><span data-stu-id="165a3-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="165a3-155">Inserte la tarjeta microSD en la Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="165a3-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="165a3-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="165a3-157">Conecte Pi al monitor, el teclado y el mouse, inicie Pi y luego inicie sesión en Raspbian con `pi` como nombre de usuario y `raspberry` como contraseña.</span><span class="sxs-lookup"><span data-stu-id="165a3-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="165a3-158">Haga clic en el icono de Raspberry > **Preferencias** > **Configuración de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="165a3-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menú Preferencias de Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="165a3-160">En la pestaña **Interfaces**, establezca **I2C** y **SSH** en **Habilitar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="165a3-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="165a3-161">Si no tiene sensores físicos y desea usar datos de detección simulados, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="165a3-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="165a3-163">Para habilitar SSH e I2C, puede buscar más documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="165a3-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="165a3-164">Conectar el sensor a Pi</span><span class="sxs-lookup"><span data-stu-id="165a3-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="165a3-165">Use la placa de pruebas y los cables de puente para conectar un LED y un BME280 a Pi como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="165a3-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="165a3-166">Si no tiene el sensor, omita esta sección.</span><span class="sxs-lookup"><span data-stu-id="165a3-166">If you don’t have the sensor, skip this section.</span></span>

![Conexión de Raspberry Pi y el sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="165a3-168">El sensor BME280 recopila datos sobre la temperatura y la humedad,</span><span class="sxs-lookup"><span data-stu-id="165a3-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="165a3-169">y el LED parpadea si se produce comunicación entre el dispositivo y la nube.</span><span class="sxs-lookup"><span data-stu-id="165a3-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="165a3-170">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="165a3-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="165a3-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="165a3-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="165a3-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="165a3-172">End (Board)</span></span>            | <span data-ttu-id="165a3-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="165a3-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="165a3-174">VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="165a3-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="165a3-175">Potencia 3,3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="165a3-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="165a3-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="165a3-176">White cable</span></span>   |
| <span data-ttu-id="165a3-177">GND (patilla 7G)</span><span class="sxs-lookup"><span data-stu-id="165a3-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="165a3-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="165a3-178">GND (Pin 6)</span></span>            | <span data-ttu-id="165a3-179">Cable marrón</span><span class="sxs-lookup"><span data-stu-id="165a3-179">Brown cable</span></span>   |
| <span data-ttu-id="165a3-180">SCK (patilla 8G)</span><span class="sxs-lookup"><span data-stu-id="165a3-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="165a3-181">I2C1 SDA (patilla 3)</span><span class="sxs-lookup"><span data-stu-id="165a3-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="165a3-182">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="165a3-182">Orange cable</span></span>  |
| <span data-ttu-id="165a3-183">SDI (patilla 10G)</span><span class="sxs-lookup"><span data-stu-id="165a3-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="165a3-184">I2C1 SCL (patilla 5)</span><span class="sxs-lookup"><span data-stu-id="165a3-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="165a3-185">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="165a3-185">Red cable</span></span>     |
| <span data-ttu-id="165a3-186">LED VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="165a3-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="165a3-187">GPIO 24 (patilla 18)</span><span class="sxs-lookup"><span data-stu-id="165a3-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="165a3-188">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="165a3-188">White cable</span></span>   |
| <span data-ttu-id="165a3-189">LED GND (patilla 17F)</span><span class="sxs-lookup"><span data-stu-id="165a3-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="165a3-190">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="165a3-190">GND (Pin 20)</span></span>           | <span data-ttu-id="165a3-191">Cable negro</span><span class="sxs-lookup"><span data-stu-id="165a3-191">Black cable</span></span>   |

<span data-ttu-id="165a3-192">Haga clic para ver [Raspberry Pi 2 & 3 Pin mappings (Asignaciones de patillas de Raspberry Pi 2 y 3)](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="165a3-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="165a3-193">Una vez que haya conectado correctamente BME280 a Raspberry Pi, su aspecto debería ser el de la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="165a3-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="165a3-195">Conexión de Pi a la red</span><span class="sxs-lookup"><span data-stu-id="165a3-195">Connect Pi to the network</span></span>

<span data-ttu-id="165a3-196">Encienda la Pi mediante un cable microUSB y la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="165a3-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="165a3-197">Use el cable Ethernet para conectar Pi a la red cableada o siga las [instrucciones de Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) para conectar Pi a la red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="165a3-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="165a3-198">Después de que Pi se ha conectado correctamente a la red, debe anotar la [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="165a3-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Conectado a la red cableada](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="165a3-200">Asegúrese de que la Pi se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="165a3-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="165a3-201">Por ejemplo, si el equipo está conectado a una red inalámbrica mientras Pi está conectada a una red cableada, es posible que no vea la dirección IP en la salida de devdisco.</span><span class="sxs-lookup"><span data-stu-id="165a3-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="165a3-202">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="165a3-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="165a3-203">Clonar una aplicación de ejemplo e instalar los paquetes de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="165a3-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="165a3-204">Use uno de los siguientes clientes SSH del equipo host para conectar con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="165a3-205">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="165a3-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="165a3-206">Necesitará la dirección IP de su Pi para conectarlo a través de SSH.</span><span class="sxs-lookup"><span data-stu-id="165a3-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="165a3-207">El cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="165a3-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="165a3-208">Quizás deba ejecutar `ssh pi@<ip address of pi>` para conectar Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="165a3-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="165a3-209">El nombre de usuario predeterminado es `pi` y la contraseña es `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="165a3-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="165a3-210">Instale Node.js y NPM en Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="165a3-211">Primero debe comprobar la versión de Node.js con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="165a3-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="165a3-212">Si la versión es inferior a 4.x o no hay ningún Node.js en el Pi, ejecute entonces el siguiente comando para instalar o actualizar Node.js.</span><span class="sxs-lookup"><span data-stu-id="165a3-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="165a3-213">Clone la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="165a3-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="165a3-214">Instale todos los paquetes mediante el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="165a3-214">Install all packages by the following command.</span></span> <span data-ttu-id="165a3-215">Incluye el SDK de dispositivo IoT de Azure, la biblioteca del sensor BME280 y la biblioteca de cableado de Pi.</span><span class="sxs-lookup"><span data-stu-id="165a3-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="165a3-216">Este proceso de instalación puede llevar varios minutos en función de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="165a3-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="165a3-217">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="165a3-217">Configure the sample application</span></span>

1. <span data-ttu-id="165a3-218">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="165a3-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="165a3-220">Hay dos elementos en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="165a3-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="165a3-221">El primero es `interval`, que define el intervalo de tiempo entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="165a3-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="165a3-222">La segunda es `simulatedData`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="165a3-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="165a3-223">Si **no tiene el sensor**, establezca el valor `simulatedData` en `true` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="165a3-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="165a3-224">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="165a3-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="165a3-225">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="165a3-225">Run the sample application</span></span>

1. <span data-ttu-id="165a3-226">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="165a3-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="165a3-227">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="165a3-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="165a3-228">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Resultado: datos de sensor enviados desde Raspberry Pi a IoT Hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="165a3-230">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="165a3-230">Next steps</span></span>

<span data-ttu-id="165a3-231">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="165a3-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]