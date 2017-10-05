---
title: 'Raspberry Pi a la nube (Node.js): Conectar Raspberry Pi a Azure IoT Hub | Microsoft Docs'
description: "Con este tutorial aprenderá a configurar y conectar Raspberry Pi a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envía datos a la nube, raspberry pi a la nube"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f48c4bd27b1df1d02090ed51172f943e50c76c3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="465d2-104">Conectar Raspberry Pi a Azure IoT Hub (Node.js)</span><span class="sxs-lookup"><span data-stu-id="465d2-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="465d2-105">En este tutorial, empezará por aprender los principios básicos del uso de Raspberry Pi que ejecuta Raspbian.</span><span class="sxs-lookup"><span data-stu-id="465d2-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="465d2-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="465d2-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="465d2-107">Para obtener ejemplos de Windows 10 IoT Core, vaya al [Centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="465d2-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="465d2-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="465d2-108">Don't have a kit yet?</span></span> <span data-ttu-id="465d2-109">Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="465d2-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="465d2-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="465d2-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="465d2-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="465d2-111">What you do</span></span>

* <span data-ttu-id="465d2-112">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="465d2-112">Create an IoT hub.</span></span>
* <span data-ttu-id="465d2-113">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="465d2-114">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="465d2-115">Ejecute una aplicación de ejemplo en Pi para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="465d2-116">Conecte Raspberry Pi al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="465d2-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="465d2-117">Luego ejecute una aplicación de ejemplo en Pi para recopilar datos de temperatura y humedad de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="465d2-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="465d2-118">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="465d2-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="465d2-119">What you learn</span></span>

* <span data-ttu-id="465d2-120">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="465d2-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="465d2-121">Cómo conectar Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="465d2-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="465d2-122">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="465d2-123">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="465d2-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="465d2-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="465d2-126">La placa de Raspberry Pi 2 o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="465d2-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="465d2-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="465d2-127">An active Azure subscription.</span></span> <span data-ttu-id="465d2-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="465d2-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="465d2-129">Un monitor, un teclado USB y un mouse que se conecten a Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="465d2-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="465d2-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="465d2-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="465d2-131">An Internet connection.</span></span>
* <span data-ttu-id="465d2-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="465d2-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="465d2-133">Un adaptador de USB a SD o una tarjeta microSD para grabar la imagen del sistema operativo en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="465d2-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="465d2-134">Una fuente de alimentación de 5 V y 2 A con un cable microUSB de 6 pies.</span><span class="sxs-lookup"><span data-stu-id="465d2-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="465d2-135">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="465d2-135">The following items are optional:</span></span>

* <span data-ttu-id="465d2-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="465d2-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="465d2-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="465d2-137">A breadboard.</span></span>
* <span data-ttu-id="465d2-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="465d2-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="465d2-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="465d2-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="465d2-140">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="465d2-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="465d2-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="465d2-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="465d2-142">Instalar el sistema operativo Raspbian para Pi</span><span class="sxs-lookup"><span data-stu-id="465d2-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="465d2-143">Prepare la tarjeta microSD para instalar la imagen de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="465d2-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="465d2-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="465d2-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="465d2-145">[Descargue Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (el archivo .zip).</span><span class="sxs-lookup"><span data-stu-id="465d2-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="465d2-146">Extraiga la imagen de Raspbian en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="465d2-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="465d2-147">Instale Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="465d2-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="465d2-148">[Descargue e instale la utilidad de grabadora de tarjetas SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="465d2-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="465d2-149">Ejecute Etcher y seleccione la imagen de Raspbian que extrajo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="465d2-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="465d2-150">Seleccione la unidad de la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="465d2-150">Select the microSD card drive.</span></span> <span data-ttu-id="465d2-151">Tenga en cuenta que es posible que Etcher ya haya seleccionado la unidad correcta.</span><span class="sxs-lookup"><span data-stu-id="465d2-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="465d2-152">Haga clic en Flash para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="465d2-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="465d2-153">Quite la tarjeta microSD del equipo cuando se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="465d2-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="465d2-154">Es seguro quitar la tarjeta microSD directamente porque Etcher expulsa o desmonta la tarjeta microSD automáticamente al acabar.</span><span class="sxs-lookup"><span data-stu-id="465d2-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="465d2-155">Inserte la tarjeta microSD en la Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="465d2-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="465d2-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="465d2-157">Conecte Pi al monitor, el teclado y el mouse, inicie Pi y luego inicie sesión en Raspbian con `pi` como nombre de usuario y `raspberry` como contraseña.</span><span class="sxs-lookup"><span data-stu-id="465d2-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="465d2-158">Haga clic en el icono de Raspberry > **Preferencias** > **Configuración de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="465d2-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menú Preferencias de Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="465d2-160">En la pestaña **Interfaces**, establezca **I2C** y **SSH** en **Habilitar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="465d2-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="465d2-161">Si no tiene sensores físicos y desea usar datos de detección simulados, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="465d2-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="465d2-163">Para habilitar SSH e I2C, puede buscar más documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="465d2-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="465d2-164">Conectar el sensor a Pi</span><span class="sxs-lookup"><span data-stu-id="465d2-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="465d2-165">Use la placa de pruebas y los cables de puente para conectar un LED y un BME280 a Pi como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="465d2-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="465d2-166">Si no tiene el sensor, [omita esta sección](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="465d2-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Conexión de Raspberry Pi y el sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="465d2-168">El sensor BME280 recopila datos sobre la temperatura y la humedad,</span><span class="sxs-lookup"><span data-stu-id="465d2-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="465d2-169">y el LED parpadea si se produce comunicación entre el dispositivo y la nube.</span><span class="sxs-lookup"><span data-stu-id="465d2-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="465d2-170">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="465d2-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="465d2-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="465d2-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="465d2-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="465d2-172">End (Board)</span></span>            | <span data-ttu-id="465d2-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="465d2-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="465d2-174">VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="465d2-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="465d2-175">Potencia 3,3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="465d2-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="465d2-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="465d2-176">White cable</span></span>   |
| <span data-ttu-id="465d2-177">GND (patilla 7G)</span><span class="sxs-lookup"><span data-stu-id="465d2-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="465d2-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="465d2-178">GND (Pin 6)</span></span>            | <span data-ttu-id="465d2-179">Cable marrón</span><span class="sxs-lookup"><span data-stu-id="465d2-179">Brown cable</span></span>   |
| <span data-ttu-id="465d2-180">SDI (patilla 10G)</span><span class="sxs-lookup"><span data-stu-id="465d2-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="465d2-181">I2C1 SDA (patilla 3)</span><span class="sxs-lookup"><span data-stu-id="465d2-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="465d2-182">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="465d2-182">Red cable</span></span>     |
| <span data-ttu-id="465d2-183">SCK (patilla 8G)</span><span class="sxs-lookup"><span data-stu-id="465d2-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="465d2-184">I2C1 SCL (patilla 5)</span><span class="sxs-lookup"><span data-stu-id="465d2-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="465d2-185">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="465d2-185">Orange cable</span></span>  |
| <span data-ttu-id="465d2-186">LED VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="465d2-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="465d2-187">GPIO 24 (patilla 18)</span><span class="sxs-lookup"><span data-stu-id="465d2-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="465d2-188">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="465d2-188">White cable</span></span>   |
| <span data-ttu-id="465d2-189">LED GND (patilla 17F)</span><span class="sxs-lookup"><span data-stu-id="465d2-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="465d2-190">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="465d2-190">GND (Pin 20)</span></span>           | <span data-ttu-id="465d2-191">Cable negro</span><span class="sxs-lookup"><span data-stu-id="465d2-191">Black cable</span></span>   |

<span data-ttu-id="465d2-192">Haga clic para ver [Raspberry Pi 2 & 3 Pin mappings (Asignaciones de patillas de Raspberry Pi 2 y 3)](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="465d2-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="465d2-193">Una vez que haya conectado correctamente BME280 a Raspberry Pi, su aspecto debería ser el de la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="465d2-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="465d2-195">Conexión de Pi a la red</span><span class="sxs-lookup"><span data-stu-id="465d2-195">Connect Pi to the network</span></span>

<span data-ttu-id="465d2-196">Encienda la Pi mediante un cable microUSB y la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="465d2-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="465d2-197">Use el cable Ethernet para conectar Pi a la red cableada o siga las [instrucciones de Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) para conectar Pi a la red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="465d2-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="465d2-198">Después de que Pi se ha conectado correctamente a la red, debe anotar la [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="465d2-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Conectado a la red cableada](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="465d2-200">Asegúrese de que la Pi se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="465d2-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="465d2-201">Por ejemplo, si el equipo está conectado a una red inalámbrica mientras Pi está conectada a una red cableada, es posible que no vea la dirección IP en la salida de devdisco.</span><span class="sxs-lookup"><span data-stu-id="465d2-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="465d2-202">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="465d2-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="465d2-203">Clonar una aplicación de ejemplo e instalar los paquetes de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="465d2-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="465d2-204">Use uno de los siguientes clientes SSH del equipo host para conectar con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="465d2-205">**Usuarios de Windows**</span><span class="sxs-lookup"><span data-stu-id="465d2-205">**Windows Users**</span></span>
   1. <span data-ttu-id="465d2-206">Descargue e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="465d2-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="465d2-207">Copie la dirección IP de Pi en la sección de nombre de host (o dirección IP) y seleccione SSH como el tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="465d2-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="465d2-209">**Usuarios de Mac y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="465d2-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="465d2-210">Use el cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="465d2-210">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="465d2-211">Quizás deba ejecutar `ssh pi@<ip address of pi>` para conectar Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="465d2-211">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="465d2-212">El nombre de usuario predeterminado es `pi` y la contraseña es `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="465d2-212">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="465d2-213">Instale Node.js y NPM en Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-213">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="465d2-214">Primero debe comprobar la versión de Node.js con el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="465d2-214">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="465d2-215">Si la versión es inferior a 4.x o no hay ningún Node.js en el Pi, ejecute entonces el siguiente comando para instalar o actualizar Node.js.</span><span class="sxs-lookup"><span data-stu-id="465d2-215">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="465d2-216">Clone la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="465d2-216">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="465d2-217">Instale todos los paquetes mediante el comando siguiente.</span><span class="sxs-lookup"><span data-stu-id="465d2-217">Install all packages by the following command.</span></span> <span data-ttu-id="465d2-218">Incluye el SDK de dispositivo IoT de Azure, la biblioteca del sensor BME280 y la biblioteca de cableado de Pi.</span><span class="sxs-lookup"><span data-stu-id="465d2-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="465d2-219">Este proceso de instalación puede llevar varios minutos en función de la conexión de red.</span><span class="sxs-lookup"><span data-stu-id="465d2-219">It might take several minutes to finish this installation process depending on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="465d2-220">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="465d2-220">Configure the sample application</span></span>

1. <span data-ttu-id="465d2-221">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="465d2-221">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="465d2-223">Hay dos elementos en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="465d2-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="465d2-224">La primera es `interval`, que define el intervalo de tiempo (en milisegundos) entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="465d2-224">The first one is `interval`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="465d2-225">La segunda es `simulatedData`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="465d2-225">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="465d2-226">Si **no tiene el sensor**, establezca el valor `simulatedData` en `true` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="465d2-226">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="465d2-227">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="465d2-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="465d2-228">Ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="465d2-228">Run the sample application</span></span>

<span data-ttu-id="465d2-229">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="465d2-229">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="465d2-230">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="465d2-230">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="465d2-231">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-231">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Resultado: datos de sensor enviados desde Raspberry Pi a IoT Hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="465d2-233">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="465d2-233">Next steps</span></span>

<span data-ttu-id="465d2-234">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="465d2-234">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="465d2-235">Para ver los mensajes que ha enviado Raspberry Pi a IoT Hub o para enviar mensajes a Raspberry Pi en una interfaz de la línea de comandos, consulte el tutorial [Administración de los mensajes de dispositivo con iothub-explorer](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="465d2-235">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
