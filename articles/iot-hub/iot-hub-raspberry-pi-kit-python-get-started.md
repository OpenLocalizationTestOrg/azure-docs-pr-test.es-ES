---
title: "Raspberry Pi en la nube (Python): conexión de Raspberry Pi a Azure IoT Hub | Microsoft Docs"
description: "Con este tutorial aprenderá a configurar y conectar Raspberry Pi a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "azure iot raspberry pi, raspberry pi iot hub, raspberry pi envía datos a la nube, raspberry pi a la nube"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="2807e-104">Conexión de Raspberry Pi a Azure IoT Hub (Python)</span><span class="sxs-lookup"><span data-stu-id="2807e-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="2807e-105">En este tutorial, empezará por aprender los principios básicos del uso de Raspberry Pi que ejecuta Raspbian.</span><span class="sxs-lookup"><span data-stu-id="2807e-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="2807e-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="2807e-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="2807e-107">Para obtener ejemplos de Windows 10 IoT Core, vaya al [Centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="2807e-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="2807e-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="2807e-108">Don't have a kit yet?</span></span> <span data-ttu-id="2807e-109">Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2807e-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="2807e-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="2807e-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="2807e-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="2807e-111">What you do</span></span>

* <span data-ttu-id="2807e-112">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="2807e-112">Create an IoT hub.</span></span>
* <span data-ttu-id="2807e-113">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="2807e-114">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2807e-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="2807e-115">Ejecute una aplicación de ejemplo en Pi para enviar datos de sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="2807e-116">Conecte Raspberry Pi al IoT Hub que ha creado.</span><span class="sxs-lookup"><span data-stu-id="2807e-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="2807e-117">Luego ejecute una aplicación de ejemplo en Pi para recopilar datos de temperatura y humedad de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="2807e-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="2807e-118">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="2807e-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="2807e-119">What you learn</span></span>

* <span data-ttu-id="2807e-120">Cómo crear Azure IoT Hub y obtener la cadena de conexión del nuevo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2807e-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="2807e-121">Cómo conectar Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="2807e-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="2807e-122">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Pi.</span><span class="sxs-lookup"><span data-stu-id="2807e-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="2807e-123">Cómo enviar los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2807e-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="2807e-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="2807e-126">La placa de Raspberry Pi 2 o Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="2807e-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="2807e-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2807e-127">An active Azure subscription.</span></span> <span data-ttu-id="2807e-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="2807e-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="2807e-129">Un monitor, un teclado USB y un mouse que se conecten a Pi.</span><span class="sxs-lookup"><span data-stu-id="2807e-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="2807e-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="2807e-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="2807e-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="2807e-131">An Internet connection.</span></span>
* <span data-ttu-id="2807e-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="2807e-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="2807e-133">Un adaptador de USB a SD o una tarjeta microSD para grabar la imagen del sistema operativo en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="2807e-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="2807e-134">Una fuente de alimentación de 5 V y 2 A con un cable microUSB de 6 pies.</span><span class="sxs-lookup"><span data-stu-id="2807e-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="2807e-135">Los elementos siguientes son opcionales:</span><span class="sxs-lookup"><span data-stu-id="2807e-135">The following items are optional:</span></span>

* <span data-ttu-id="2807e-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="2807e-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="2807e-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="2807e-137">A breadboard.</span></span>
* <span data-ttu-id="2807e-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="2807e-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="2807e-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="2807e-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="2807e-140">Estos elementos son opcionales porque el ejemplo de código simula los datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="2807e-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="2807e-141">Configuración de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="2807e-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="2807e-142">Instalar el sistema operativo Raspbian para Pi</span><span class="sxs-lookup"><span data-stu-id="2807e-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="2807e-143">Prepare la tarjeta microSD para instalar la imagen de Raspbian.</span><span class="sxs-lookup"><span data-stu-id="2807e-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="2807e-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="2807e-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="2807e-145">[Descargue Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (el archivo .zip).</span><span class="sxs-lookup"><span data-stu-id="2807e-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="2807e-146">Extraiga la imagen de Raspbian en una carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="2807e-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="2807e-147">Instale Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="2807e-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="2807e-148">[Descargue e instale la utilidad de grabadora de tarjetas SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="2807e-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="2807e-149">Ejecute Etcher y seleccione la imagen de Raspbian que extrajo en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="2807e-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="2807e-150">Seleccione la unidad de la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="2807e-150">Select the microSD card drive.</span></span> <span data-ttu-id="2807e-151">Tenga en cuenta que es posible que Etcher ya haya seleccionado la unidad correcta.</span><span class="sxs-lookup"><span data-stu-id="2807e-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="2807e-152">Haga clic en Flash para instalar Raspbian en la tarjeta microSD.</span><span class="sxs-lookup"><span data-stu-id="2807e-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="2807e-153">Quite la tarjeta microSD del equipo cuando se complete la instalación.</span><span class="sxs-lookup"><span data-stu-id="2807e-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="2807e-154">Es seguro quitar la tarjeta microSD directamente porque Etcher expulsa o desmonta la tarjeta microSD automáticamente al acabar.</span><span class="sxs-lookup"><span data-stu-id="2807e-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="2807e-155">Inserte la tarjeta microSD en la Pi.</span><span class="sxs-lookup"><span data-stu-id="2807e-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="2807e-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="2807e-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="2807e-157">Conecte Pi al monitor, el teclado y el mouse, inicie Pi y luego inicie sesión en Raspbian con `pi` como nombre de usuario y `raspberry` como contraseña.</span><span class="sxs-lookup"><span data-stu-id="2807e-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="2807e-158">Haga clic en el icono de Raspberry > **Preferencias** > **Configuración de Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="2807e-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menú Preferencias de Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="2807e-160">En la pestaña **Interfaces**, establezca **I2C** y **SSH** en **Habilitar** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2807e-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="2807e-161">Si no tiene sensores físicos y desea usar datos de detección simulados, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="2807e-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="2807e-163">Para habilitar SSH e I2C, puede buscar más documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="2807e-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="2807e-164">Conectar el sensor a Pi</span><span class="sxs-lookup"><span data-stu-id="2807e-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="2807e-165">Use la placa de pruebas y los cables de puente para conectar un LED y un BME280 a Pi como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="2807e-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="2807e-166">Si no tiene el sensor, [omita esta sección](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="2807e-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Conexión de Raspberry Pi y el sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="2807e-168">El sensor BME280 recopila datos sobre la temperatura y la humedad,</span><span class="sxs-lookup"><span data-stu-id="2807e-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="2807e-169">y el LED parpadea si se produce comunicación entre el dispositivo y la nube.</span><span class="sxs-lookup"><span data-stu-id="2807e-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="2807e-170">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="2807e-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="2807e-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="2807e-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="2807e-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="2807e-172">End (Board)</span></span>            | <span data-ttu-id="2807e-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="2807e-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="2807e-174">VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="2807e-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="2807e-175">Potencia 3,3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="2807e-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="2807e-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="2807e-176">White cable</span></span>   |
| <span data-ttu-id="2807e-177">GND (patilla 7G)</span><span class="sxs-lookup"><span data-stu-id="2807e-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="2807e-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="2807e-178">GND (Pin 6)</span></span>            | <span data-ttu-id="2807e-179">Cable marrón</span><span class="sxs-lookup"><span data-stu-id="2807e-179">Brown cable</span></span>   |
| <span data-ttu-id="2807e-180">SDI (patilla 10G)</span><span class="sxs-lookup"><span data-stu-id="2807e-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="2807e-181">I2C1 SDA (patilla 3)</span><span class="sxs-lookup"><span data-stu-id="2807e-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="2807e-182">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="2807e-182">Red cable</span></span>     |
| <span data-ttu-id="2807e-183">SCK (patilla 8G)</span><span class="sxs-lookup"><span data-stu-id="2807e-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="2807e-184">I2C1 SCL (patilla 5)</span><span class="sxs-lookup"><span data-stu-id="2807e-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="2807e-185">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="2807e-185">Orange cable</span></span>  |
| <span data-ttu-id="2807e-186">LED VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="2807e-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="2807e-187">GPIO 24 (patilla 18)</span><span class="sxs-lookup"><span data-stu-id="2807e-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="2807e-188">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="2807e-188">White cable</span></span>   |
| <span data-ttu-id="2807e-189">LED GND (patilla 17F)</span><span class="sxs-lookup"><span data-stu-id="2807e-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="2807e-190">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="2807e-190">GND (Pin 20)</span></span>           | <span data-ttu-id="2807e-191">Cable negro</span><span class="sxs-lookup"><span data-stu-id="2807e-191">Black cable</span></span>   |

<span data-ttu-id="2807e-192">Haga clic para ver [Raspberry Pi 2 & 3 Pin mappings (Asignaciones de patillas de Raspberry Pi 2 y 3)](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="2807e-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="2807e-193">Una vez que haya conectado correctamente BME280 a Raspberry Pi, su aspecto debería ser el de la imagen siguiente.</span><span class="sxs-lookup"><span data-stu-id="2807e-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="2807e-195">Conexión de Pi a la red</span><span class="sxs-lookup"><span data-stu-id="2807e-195">Connect Pi to the network</span></span>

<span data-ttu-id="2807e-196">Encienda la Pi mediante un cable microUSB y la fuente de alimentación.</span><span class="sxs-lookup"><span data-stu-id="2807e-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="2807e-197">Use el cable Ethernet para conectar Pi a la red cableada o siga las [instrucciones de Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) para conectar Pi a la red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="2807e-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="2807e-198">Después de que Pi se ha conectado correctamente a la red, debe anotar la [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="2807e-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Conectado a la red cableada](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="2807e-200">Asegúrese de que la Pi se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="2807e-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="2807e-201">Por ejemplo, si el equipo está conectado a una red inalámbrica mientras Pi está conectada a una red cableada, es posible que no vea la dirección IP en la salida de devdisco.</span><span class="sxs-lookup"><span data-stu-id="2807e-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="2807e-202">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="2807e-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="2807e-203">Instalar los paquetes de requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2807e-203">Install the prerequisite packages</span></span>

<span data-ttu-id="2807e-204">Use uno de los siguientes clientes SSH del equipo host para conectar con Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="2807e-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="2807e-205">**Usuarios de Windows**</span><span class="sxs-lookup"><span data-stu-id="2807e-205">**Windows Users**</span></span>
   1. <span data-ttu-id="2807e-206">Descargue e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="2807e-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="2807e-207">Copie la dirección IP de Pi en la sección de nombre de host (o dirección IP) y seleccione SSH como el tipo de conexión.</span><span class="sxs-lookup"><span data-stu-id="2807e-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="2807e-208">**Usuarios de Mac y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2807e-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="2807e-209">Use el cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="2807e-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="2807e-210">Quizás deba ejecutar `ssh pi@<ip address of pi>` para conectar Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="2807e-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="2807e-211">El nombre de usuario predeterminado es `pi` y la contraseña es `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="2807e-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="2807e-212">Configurar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2807e-212">Configure the sample application</span></span>

1. <span data-ttu-id="2807e-213">Clone la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="2807e-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="2807e-214">Abra el archivo config mediante la ejecución de los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="2807e-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="2807e-215">Hay cinco macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="2807e-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="2807e-216">La primera es `MESSAGE_TIMESPAN`, que define el intervalo de tiempo (en milisegundos) entre dos mensajes que se envían a la nube.</span><span class="sxs-lookup"><span data-stu-id="2807e-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="2807e-217">La segunda es `SIMULATED_DATA`, un valor booleano que indica si se usan los datos de sensor simulados o no.</span><span class="sxs-lookup"><span data-stu-id="2807e-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="2807e-218">`I2C_ADDRESS` es la dirección de I2C a la que está conectado el sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="2807e-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="2807e-219">`GPIO_PIN_ADDRESS` es la dirección GPIO del LED.</span><span class="sxs-lookup"><span data-stu-id="2807e-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="2807e-220">La última de ellas es `BLINK_TIMESPAN`, que define el intervalo de tiempo cuando se activa el LED en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="2807e-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="2807e-221">Si **no tiene el sensor**, establezca el valor `SIMULATED_DATA` en `True` para que la aplicación de ejemplo cree y use datos de sensor simulados.</span><span class="sxs-lookup"><span data-stu-id="2807e-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="2807e-222">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="2807e-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="2807e-223">Compilar y ejecutar la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2807e-223">Build and run the sample application</span></span>

1. <span data-ttu-id="2807e-224">Compile la aplicación de ejemplo con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="2807e-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="2807e-225">Dado que los SDK de Azure IoT para Python son contenedores que funcionan sobre el SDK de C de dispositivos de Azure IoT, debe compilar las bibliotecas de C si desea o necesita generar las bibliotecas de Python a partir del código fuente.</span><span class="sxs-lookup"><span data-stu-id="2807e-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="2807e-226">También puede especificar la versión que quiere mediante la ejecución de `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="2807e-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="2807e-227">Si ejecuta el script sin parámetros, este detecta automáticamente la versión de Python instalada (secuencia de búsqueda 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="2807e-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="2807e-228">Asegúrese de que su versión de Python mantenga la coherencia durante la compilación y la ejecución.</span><span class="sxs-lookup"><span data-stu-id="2807e-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="2807e-229">Al compilar la biblioteca de cliente de Python (iothub_client.so) en dispositivos Linux que tienen menos de 1 GB de RAM, puede ver que la operación se queda atascada en el 98 % mientras se compila iothub_client_python.cpp, como se muestra a continuación `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="2807e-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="2807e-230">Si experimenta este problema, compruebe el consumo de memoria del dispositivo usando `free -m command` en otra ventana de terminal durante ese tiempo.</span><span class="sxs-lookup"><span data-stu-id="2807e-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="2807e-231">Si se queda sin memoria mientras compila el archivo iothub_client_python.cpp, puede que tenga que aumentar temporalmente el espacio de intercambio para obtener más memoria disponible y así compilar correctamente la biblioteca del SDK del dispositivo cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="2807e-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="2807e-232">Ejecute la aplicación de ejemplo mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="2807e-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="2807e-233">Asegúrese de que copia y pega la cadena de conexión del dispositivo entre las comillas simples.</span><span class="sxs-lookup"><span data-stu-id="2807e-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="2807e-234">Y si usa la versión 3 de Python, puede utilizar el comando `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="2807e-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="2807e-235">Debería ver el resultado siguiente, que muestra los datos del sensor y los mensajes que se envían a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Resultado: datos de sensor enviados desde Raspberry Pi a IoT Hub](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="2807e-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2807e-237">Next steps</span></span>

<span data-ttu-id="2807e-238">Ha ejecutado una aplicación de ejemplo para recopilar datos de sensor y enviarlos a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2807e-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="2807e-239">Para ver los mensajes que ha enviado Raspberry Pi a IoT Hub o para enviar mensajes a Raspberry Pi en una interfaz de la línea de comandos, consulte el tutorial [Administración de los mensajes de dispositivo con iothub-explorer](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="2807e-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
