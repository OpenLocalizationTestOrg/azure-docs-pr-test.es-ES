---
title: 'Raspberry Pi en la nube (C): Conectar Raspberry Pi a Azure IoT Hub | Microsoft Docs'
description: "Con este tutorial aprenderá a configurar y conectar Raspberry Pi a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envía datos a la nube, raspberry pi a la nube"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8b8fda17a8d1d1796d5299e3aba4b0fd5e719a4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-c"></a><span data-ttu-id="0c815-104">Conectar Raspberry Pi a Azure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="0c815-104">Connect Raspberry Pi to Azure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0c815-105">En este tutorial, empezará por aprender los principios básicos del uso de Raspberry Pi que ejecuta Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c815-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="0c815-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="0c815-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="0c815-107">Para obtener ejemplos de Windows 10 IoT Core, vaya al [Centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="0c815-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="0c815-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="0c815-108">Don't have a kit yet?</span></span> <span data-ttu-id="0c815-109">Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c815-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="0c815-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="0c815-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0c815-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="0c815-111">What you do</span></span>

* <span data-ttu-id="0c815-112">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="0c815-112">Create an IoT hub.</span></span>
* <span data-ttu-id="0c815-113">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="0c815-114">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c815-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="0c815-115">Ejecute una aplicación de ejemplo en Pi para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="0c815-116">Conecte Raspberry Pi al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="0c815-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="0c815-117">Luego ejecute una aplicación de ejemplo en Pi para recopilar datos de temperatura y humedad de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="0c815-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="0c815-118">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0c815-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="0c815-119">What you learn</span></span>

* <span data-ttu-id="0c815-120">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0c815-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="0c815-121">Cómo conectar Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="0c815-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="0c815-122">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="0c815-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="0c815-123">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0c815-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="0c815-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="0c815-126">La placa de Raspberry Pi 2 o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="0c815-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="0c815-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="0c815-127">An active Azure subscription.</span></span> <span data-ttu-id="0c815-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0c815-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0c815-129">Un monitor, un teclado USB y un mouse que se conecten a Pi.</span><span class="sxs-lookup"><span data-stu-id="0c815-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="0c815-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="0c815-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="0c815-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="0c815-131">An Internet connection.</span></span>
* <span data-ttu-id="0c815-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="0c815-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="0c815-133">Un adaptador de USB a SD o una tarjeta microSD para grabar la imagen del sistema operativo en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="0c815-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="0c815-134">Una fuente de alimentación de 5 V y 2 A con un cable microUSB de 6 pies.</span><span class="sxs-lookup"><span data-stu-id="0c815-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="0c815-135">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="0c815-135">The following items are optional:</span></span>

* <span data-ttu-id="0c815-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="0c815-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="0c815-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="0c815-137">A breadboard.</span></span>
* <span data-ttu-id="0c815-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="0c815-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="0c815-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="0c815-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="0c815-140">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="0c815-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="0c815-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="0c815-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="0c815-142">Instalar el sistema operativo Raspbian para Pi</span><span class="sxs-lookup"><span data-stu-id="0c815-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="0c815-143">Prepare la tarjeta microSD para instalar la imagen de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c815-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="0c815-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c815-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="0c815-145">[Descargue Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (el archivo .zip).</span><span class="sxs-lookup"><span data-stu-id="0c815-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="0c815-146">Extraiga la imagen de Raspbian en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="0c815-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="0c815-147">Instale Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="0c815-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="0c815-148">[Descargue e instale la utilidad de grabadora de tarjetas SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="0c815-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="0c815-149">Ejecute Etcher y seleccione la imagen de Raspbian que extrajo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="0c815-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="0c815-150">Seleccione la unidad de la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="0c815-150">Select the microSD card drive.</span></span> <span data-ttu-id="0c815-151">Tenga en cuenta que es posible que Etcher ya haya seleccionado la unidad correcta.</span><span class="sxs-lookup"><span data-stu-id="0c815-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="0c815-152">Haga clic en Flash para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="0c815-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="0c815-153">Quite la tarjeta microSD del equipo cuando se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="0c815-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="0c815-154">Es seguro quitar la tarjeta microSD directamente porque Etcher expulsa o desmonta la tarjeta microSD automáticamente al acabar.</span><span class="sxs-lookup"><span data-stu-id="0c815-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="0c815-155">Inserte la tarjeta microSD en la Pi.</span><span class="sxs-lookup"><span data-stu-id="0c815-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="0c815-156">Habilitar SSH y SPI</span><span class="sxs-lookup"><span data-stu-id="0c815-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="0c815-157">Conecte Pi al monitor, el teclado y el mouse, inicie Pi y luego inicie sesión en Raspbian con `pi` como nombre de usuario y `raspberry` como contraseña.</span><span class="sxs-lookup"><span data-stu-id="0c815-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="0c815-158">Haga clic en el icono de Raspberry > **Preferencias** > **Configuración de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="0c815-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menú Preferencias de Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="0c815-160">En la pestaña **Interfaces**, establezca **SPI** y **SSH** en **Habilitar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0c815-160">On the **Interfaces** tab, set **SPI** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="0c815-161">Si no tiene sensores físicos y desea usar datos de detección simulados, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="0c815-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Habilitar SPI y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="0c815-163">Para habilitar SSH y SPI, puede buscar más documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="0c815-163">To enable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="0c815-164">Conectar el sensor a Pi</span><span class="sxs-lookup"><span data-stu-id="0c815-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="0c815-165">Use la placa de pruebas y los cables de puente para conectar un LED y un BME280 a Pi como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="0c815-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="0c815-166">Si no tiene el sensor, [omita esta sección](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="0c815-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Conexión de Raspberry Pi y el sensor](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="0c815-168">El sensor BME280 recopila datos sobre la temperatura y la humedad,</span><span class="sxs-lookup"><span data-stu-id="0c815-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="0c815-169">y el LED parpadea si se produce comunicación entre el dispositivo y la nube.</span><span class="sxs-lookup"><span data-stu-id="0c815-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="0c815-170">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="0c815-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="0c815-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="0c815-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="0c815-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="0c815-172">End (Board)</span></span>            | <span data-ttu-id="0c815-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="0c815-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="0c815-174">LED VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="0c815-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="0c815-175">GPIO 4 (patilla 7)</span><span class="sxs-lookup"><span data-stu-id="0c815-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="0c815-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="0c815-176">White cable</span></span>   |
| <span data-ttu-id="0c815-177">LED GND (patilla 6G)</span><span class="sxs-lookup"><span data-stu-id="0c815-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="0c815-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="0c815-178">GND (Pin 6)</span></span>            | <span data-ttu-id="0c815-179">Cable negro</span><span class="sxs-lookup"><span data-stu-id="0c815-179">Black cable</span></span>   |
| <span data-ttu-id="0c815-180">VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="0c815-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="0c815-181">Potencia 3,3 V (patilla 17)</span><span class="sxs-lookup"><span data-stu-id="0c815-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="0c815-182">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="0c815-182">White cable</span></span>   |
| <span data-ttu-id="0c815-183">GND (patilla 20F)</span><span class="sxs-lookup"><span data-stu-id="0c815-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="0c815-184">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="0c815-184">GND (Pin 20)</span></span>           | <span data-ttu-id="0c815-185">Cable negro</span><span class="sxs-lookup"><span data-stu-id="0c815-185">Black cable</span></span>   |
| <span data-ttu-id="0c815-186">SCK (patilla 21F)</span><span class="sxs-lookup"><span data-stu-id="0c815-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="0c815-187">SPI0 SCLK (patilla 23)</span><span class="sxs-lookup"><span data-stu-id="0c815-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="0c815-188">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="0c815-188">Orange cable</span></span>  |
| <span data-ttu-id="0c815-189">SDO (patilla 22F)</span><span class="sxs-lookup"><span data-stu-id="0c815-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="0c815-190">SPI0 MISO (patilla 21)</span><span class="sxs-lookup"><span data-stu-id="0c815-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="0c815-191">Cable amarillo</span><span class="sxs-lookup"><span data-stu-id="0c815-191">Yellow cable</span></span>  |
| <span data-ttu-id="0c815-192">SDI (patilla 23F)</span><span class="sxs-lookup"><span data-stu-id="0c815-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="0c815-193">SPI0 MOSI (patilla 19)</span><span class="sxs-lookup"><span data-stu-id="0c815-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="0c815-194">Cable verde</span><span class="sxs-lookup"><span data-stu-id="0c815-194">Green cable</span></span>   |
| <span data-ttu-id="0c815-195">CS (patilla 24F)</span><span class="sxs-lookup"><span data-stu-id="0c815-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="0c815-196">SPI0 CS (patilla 24)</span><span class="sxs-lookup"><span data-stu-id="0c815-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="0c815-197">Cable azul</span><span class="sxs-lookup"><span data-stu-id="0c815-197">Blue cable</span></span>    |

<span data-ttu-id="0c815-198">Haga clic para ver [Raspberry Pi 2 & 3 Pin mappings (Asignaciones de patillas de Raspberry Pi 2 y 3)](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="0c815-198">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="0c815-199">Una vez que haya conectado correctamente BME280 a Raspberry Pi, su aspecto debería ser el de la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="0c815-199">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="0c815-201">Conexión de Pi a la red</span><span class="sxs-lookup"><span data-stu-id="0c815-201">Connect Pi to the network</span></span>

<span data-ttu-id="0c815-202">Encienda la Pi mediante un cable microUSB y la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="0c815-202">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="0c815-203">Use el cable Ethernet para conectar Pi a la red cableada o siga las [instrucciones de Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) para conectar Pi a la red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="0c815-203">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="0c815-204">Después de que Pi se ha conectado correctamente a la red, debe anotar la [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="0c815-204">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Conectado a la red cableada](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="0c815-206">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="0c815-206">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="0c815-207">Instalar los paquetes de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0c815-207">Install the prerequisite packages</span></span>

1. <span data-ttu-id="0c815-208">Use uno de los siguientes clientes SSH del equipo host para conectar con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="0c815-208">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="0c815-209">**Usuarios de Windows**</span><span class="sxs-lookup"><span data-stu-id="0c815-209">**Windows Users**</span></span>
   1. <span data-ttu-id="0c815-210">Descargue e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="0c815-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="0c815-211">Copie la dirección IP de Pi en la sección de nombre de host (o dirección IP) y seleccione SSH como el tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="0c815-211">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="0c815-213">**Usuarios de Mac y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="0c815-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="0c815-214">Use el cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="0c815-214">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="0c815-215">Quizás deba ejecutar `ssh pi@<ip address of pi>` para conectar Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="0c815-215">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="0c815-216">El nombre de usuario predeterminado es `pi` y la contraseña es `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="0c815-216">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="0c815-217">Instale los paquetes de requisitos previos para el SDK de dispositivo IoT de Microsoft Azure para C y Cmake al ejecutar los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0c815-217">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C and Cmake by running the following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-the-sample-application"></a><span data-ttu-id="0c815-218">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0c815-218">Configure the sample application</span></span>

1. <span data-ttu-id="0c815-219">Clone la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0c815-219">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="0c815-220">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="0c815-220">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="0c815-222">Hay dos macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="0c815-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="0c815-223">La primera es `INTERVAL`, que define el intervalo de tiempo (en milisegundos) entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="0c815-223">The first one is `INTERVAL`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="0c815-224">La segunda es `SIMULATED_DATA`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="0c815-224">The second one `SIMULATED_DATA`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="0c815-225">Si **no tiene el sensor**, establezca el valor `SIMULATED_DATA` en `1` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="0c815-225">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `1` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="0c815-226">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="0c815-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="0c815-227">Compilar y ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0c815-227">Build and run the sample application</span></span>

1. <span data-ttu-id="0c815-228">Compile la aplicación de ejemplo al ejecutar el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0c815-228">Build the sample application by running the following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Resultado de la compilación](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="0c815-230">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="0c815-230">Run the sample application by running the following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="0c815-231">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="0c815-231">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="0c815-232">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-232">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Resultado: datos de sensor enviados desde Raspberry Pi a IoT Hub](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="0c815-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0c815-234">Next steps</span></span>

<span data-ttu-id="0c815-235">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c815-235">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="0c815-236">Para ver los mensajes que ha enviado Raspberry Pi a IoT Hub o para enviar mensajes a Raspberry Pi en una interfaz de la línea de comandos, consulte el tutorial [Administración de los mensajes de dispositivo con iothub-explorer](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="0c815-236">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
