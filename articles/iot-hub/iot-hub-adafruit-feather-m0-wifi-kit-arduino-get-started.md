---
title: "M0 a la nube: conexión de Feather M0 WiFi a Azure IoT Hub | Microsoft Docs"
description: "Con este tutorial aprenderá a configurar y conectar Adafruit Feather M0 WiFi a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="18379-103">Conectar Adafruit Feather M0 WiFi a Azure IoT Hub en la nube</span><span class="sxs-lookup"><span data-stu-id="18379-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre BME280, Feather M0 WiFi e IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="18379-105">En este tutorial, empiece por aprender los conceptos básicos sobre cómo trabajar con la placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="18379-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="18379-106">A continuación, aprenderá a conectar sin problemas los dispositivos en la nube con [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="18379-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="18379-107">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="18379-107">What you do</span></span>

<span data-ttu-id="18379-108">Conecte Adafruit Feather M0 WiFi a un IoT Hub que cree.</span><span class="sxs-lookup"><span data-stu-id="18379-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="18379-109">Luego ejecute una aplicación de ejemplo en M0 WiFi para recopilar datos de temperatura y humedad de un BME280.</span><span class="sxs-lookup"><span data-stu-id="18379-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="18379-110">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="18379-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="18379-111">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="18379-111">What you learn</span></span>

* <span data-ttu-id="18379-112">Cómo crear un IoT Hub y registrar un dispositivo en Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="18379-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="18379-113">Cómo conectar Feather M0 WiFi con el sensor y el equipo</span><span class="sxs-lookup"><span data-stu-id="18379-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="18379-114">Cómo recopilar datos del sensor al ejecutar una aplicación de ejemplo en Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="18379-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="18379-115">Cómo enviar los datos del sensor a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="18379-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="18379-116">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="18379-116">What you need</span></span>

![Elementos necesarios para el tutorial](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="18379-118">Para realizar esta operación, necesita los siguientes elementos del kit de inicio de Feather M0 WiFi:</span><span class="sxs-lookup"><span data-stu-id="18379-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="18379-119">La placa Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="18379-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="18379-120">Un cable micro USB a USB tipo A</span><span class="sxs-lookup"><span data-stu-id="18379-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="18379-121">También necesitará lo siguiente para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="18379-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="18379-122">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="18379-122">An active Azure subscription.</span></span> <span data-ttu-id="18379-123">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="18379-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="18379-124">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="18379-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="18379-125">Una red inalámbrica a la que conectar Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="18379-126">Conexión a Internet para descargar la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="18379-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="18379-127">[IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="18379-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="18379-128">Las versiones anteriores no funcionan con la biblioteca de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="18379-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="18379-129">Los elementos siguientes son opcionales en caso de que no tenga sensor.</span><span class="sxs-lookup"><span data-stu-id="18379-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="18379-130">También tiene la opción de usar datos del sensor simulados:</span><span class="sxs-lookup"><span data-stu-id="18379-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="18379-131">Un sensor de temperatura y humedad BME280</span><span class="sxs-lookup"><span data-stu-id="18379-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="18379-132">Una placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="18379-132">A breadboard</span></span>
* <span data-ttu-id="18379-133">Cables de puente M/M</span><span class="sxs-lookup"><span data-stu-id="18379-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="18379-134">Conectar Feather M0 WiFi con el sensor y el equipo</span><span class="sxs-lookup"><span data-stu-id="18379-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="18379-135">En esta sección se conectan los sensores a la placa.</span><span class="sxs-lookup"><span data-stu-id="18379-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="18379-136">Luego se conecta el dispositivo al equipo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="18379-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="18379-137">Conectar un sensor de humedad y temperatura DHT22 a Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="18379-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="18379-138">Use la placa de pruebas y los cables de puente para realizar la conexión.</span><span class="sxs-lookup"><span data-stu-id="18379-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="18379-139">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="18379-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referencia de conexiones](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="18379-141">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="18379-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="18379-142">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="18379-142">Start (sensor)</span></span>           | <span data-ttu-id="18379-143">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="18379-143">End (board)</span></span>            | <span data-ttu-id="18379-144">Color del cable</span><span class="sxs-lookup"><span data-stu-id="18379-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="18379-145">VDD (patilla 27A)</span><span class="sxs-lookup"><span data-stu-id="18379-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="18379-146">3V (patilla 3A)</span><span class="sxs-lookup"><span data-stu-id="18379-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="18379-147">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="18379-147">Red cable</span></span>     |
| <span data-ttu-id="18379-148">GND (patilla 29A)</span><span class="sxs-lookup"><span data-stu-id="18379-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="18379-149">GND (patilla 6A)</span><span class="sxs-lookup"><span data-stu-id="18379-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="18379-150">Cable negro</span><span class="sxs-lookup"><span data-stu-id="18379-150">Black cable</span></span>   |
| <span data-ttu-id="18379-151">SCK (patilla 30A)</span><span class="sxs-lookup"><span data-stu-id="18379-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="18379-152">SCK (patilla 12A)</span><span class="sxs-lookup"><span data-stu-id="18379-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="18379-153">Cable amarillo</span><span class="sxs-lookup"><span data-stu-id="18379-153">Yellow cable</span></span>  |
| <span data-ttu-id="18379-154">SDO (patilla 31A)</span><span class="sxs-lookup"><span data-stu-id="18379-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="18379-155">MI (patilla 14A)</span><span class="sxs-lookup"><span data-stu-id="18379-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="18379-156">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="18379-156">White cable</span></span>   |
| <span data-ttu-id="18379-157">SDI (patilla 32A)</span><span class="sxs-lookup"><span data-stu-id="18379-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="18379-158">M0 (patilla 13A)</span><span class="sxs-lookup"><span data-stu-id="18379-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="18379-159">Cable azul</span><span class="sxs-lookup"><span data-stu-id="18379-159">Blue cable</span></span>    |
| <span data-ttu-id="18379-160">CS (patilla 33A)</span><span class="sxs-lookup"><span data-stu-id="18379-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="18379-161">GPIO 5 (patilla 15J)</span><span class="sxs-lookup"><span data-stu-id="18379-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="18379-162">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="18379-162">Orange cable</span></span>  |

<span data-ttu-id="18379-163">Para más información, consulte la [introducción al sensor de presión atmosférica, temperatura y humedad Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) y el artículo sobre el [patillaje de Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="18379-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="18379-164">Ahora Feather M0 WiFi debe estar conectado con un sensor en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="18379-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Conectar DHT22 con Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="18379-166">Conectar Feather M0 WiFi al equipo</span><span class="sxs-lookup"><span data-stu-id="18379-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="18379-167">Use el cable micro USB a USB tipo A para conectar Feather M0 WiFi al equipo, tal y como se muestra:</span><span class="sxs-lookup"><span data-stu-id="18379-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![Conectar Feather Huzzah al equipo](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="18379-169">Agregar permisos de puerto serie (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="18379-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="18379-170">Si usa Ubuntu, asegúrese de que tiene los permisos necesarios para trabajar en el puerto USB de Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="18379-171">Para agregar permisos de puerto serie, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="18379-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="18379-172">En el terminal, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="18379-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="18379-173">Obtendrá una de las siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="18379-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="18379-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="18379-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="18379-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="18379-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="18379-176">En la salida, observe que `uucp` o `dialout` es el nombre del propietario del grupo del puerto USB.</span><span class="sxs-lookup"><span data-stu-id="18379-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="18379-177">Agregue el usuario al grupo, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="18379-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="18379-178">En el paso anterior obtuvo el nombre del propietario del grupo, `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="18379-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="18379-179">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="18379-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="18379-180">Para que aparezca el cambio, cierre la sesión de Ubuntu y vuelva a iniciarla.</span><span class="sxs-lookup"><span data-stu-id="18379-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="18379-181">Recopilación de datos del sensor y envío al centro de IoT</span><span class="sxs-lookup"><span data-stu-id="18379-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="18379-182">En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="18379-183">La aplicación de ejemplo hace que el LED de Feather M0 WiFi parpadee.</span><span class="sxs-lookup"><span data-stu-id="18379-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="18379-184">A continuación, envía los datos de temperatura y humedad recopilados del sensor BME280 a la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="18379-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="18379-185">Obtención de la aplicación de ejemplo de Github y preparación del IDE de Arduino</span><span class="sxs-lookup"><span data-stu-id="18379-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="18379-186">La aplicación de ejemplo se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="18379-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="18379-187">Clone el repositorio de ejemplos que contiene la aplicación de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="18379-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="18379-188">Para clonar el repositorio de ejemplos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="18379-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="18379-189">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="18379-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="18379-190">Vaya a la carpeta donde desea almacenar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="18379-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="18379-191">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="18379-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="18379-192">Instalación del paquete de Feather M0 WiFi en el IDE de Arduino</span><span class="sxs-lookup"><span data-stu-id="18379-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="18379-193">Abra la carpeta donde se almacena la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="18379-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="18379-194">Abra el archivo app.ino en la carpeta de la aplicación en el IDE de Arduino.</span><span class="sxs-lookup"><span data-stu-id="18379-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Abrir la aplicación de ejemplo en el IDE de Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="18379-196">Haga clic en **File** (Archivo) > **Preferences** (Preferencias) (Windows o Linux) o **Arduino** > **Preferences** (Preferencias) (Mac), y copie y pegue el vínculo en la opción **Additional Boards Manager URLs** (Direcciones URL del administrador de placas adicionales) de las preferencias de IDE de Arduino.</span><span class="sxs-lookup"><span data-stu-id="18379-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="18379-197">Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Boards Manager** (Administrador de placas) y luego instale `Arduino SAMD Boards` versión `1.6.2` o posterior.</span><span class="sxs-lookup"><span data-stu-id="18379-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="18379-198">Después, en la misma ventana, instale el paquete `Adafruit SAMD Boards` para agregar las definiciones de archivo de la placa.</span><span class="sxs-lookup"><span data-stu-id="18379-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![Se instala el paquete esp8266](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="18379-200">Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="18379-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="18379-201">Instale los controladores (solo para Windows).</span><span class="sxs-lookup"><span data-stu-id="18379-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="18379-202">Al conectar Feather M0 WiFi, quizá deba instalar un controlador.</span><span class="sxs-lookup"><span data-stu-id="18379-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="18379-203">Haga clic en el [vínculo de descarga de la página web](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) para descargar el instalador de controladores.</span><span class="sxs-lookup"><span data-stu-id="18379-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="18379-204">Siga los pasos para instalar los controladores que quiera instalar.</span><span class="sxs-lookup"><span data-stu-id="18379-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="18379-205">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="18379-205">Install necessary libraries</span></span>

1. <span data-ttu-id="18379-206">En Arduino IDE, haga clic en **Sketch** >  (Boceto) **Include Library** >  (Incluir biblioteca) **Manage Libraries** (Administrar bibliotecas).</span><span class="sxs-lookup"><span data-stu-id="18379-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="18379-207">Busque los nombres de biblioteca siguientes uno a uno.</span><span class="sxs-lookup"><span data-stu-id="18379-207">Search for the following library names one by one.</span></span> <span data-ttu-id="18379-208">Para cada biblioteca que encuentre, haga clic en **Install** (Instalar):</span><span class="sxs-lookup"><span data-stu-id="18379-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="18379-209">Instale manualmente `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="18379-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="18379-210">Vaya a [este sitio web](https://github.com/adafruit/Adafruit_WINC1500) y haga clic en **Clone or download** (Clonar o descargar) > **Download ZIP** (Descargar archivo ZIP).</span><span class="sxs-lookup"><span data-stu-id="18379-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="18379-211">Después, en el IDE de Arduino, vaya a **Sketch** (Boceto) > **Include Library** (Incluir biblioteca) > **Add .zip Library** (Incluir biblioteca de archivos ZIP) y agregue el archivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="18379-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="18379-212">Use la aplicación de ejemplo si no dispone de un sensor BME280 real</span><span class="sxs-lookup"><span data-stu-id="18379-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="18379-213">Si no tiene un sensor BME280 real, la aplicación de ejemplo puede simular datos de humedad y temperatura.</span><span class="sxs-lookup"><span data-stu-id="18379-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="18379-214">Para configurar la aplicación de ejemplo de modo que use datos simulados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="18379-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="18379-215">Abra el archivo `config.h` de la carpeta `app`.</span><span class="sxs-lookup"><span data-stu-id="18379-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="18379-216">Busque la siguiente línea de código y cambie el valor de `false` a `true`:</span><span class="sxs-lookup"><span data-stu-id="18379-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar la aplicación de ejemplo para usar datos simulados](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="18379-218">Guarde el archivo como `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="18379-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="18379-219">Implementar la aplicación de ejemplo en Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="18379-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="18379-220">En el IDE de Arduino, haga clic en **Tool** (Herramienta)  > **Port** (Puerto) y luego en el puerto serie de Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="18379-221">Haga clic en **Sketch** (Boceto)  > **Upload** (Cargar) para compilar e implementar la aplicación de ejemplo en Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="18379-222">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="18379-222">Enter your credentials</span></span>

<span data-ttu-id="18379-223">Cuando la carga finalice correctamente, siga estos pasos para escribir las credenciales:</span><span class="sxs-lookup"><span data-stu-id="18379-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="18379-224">En Arduino IDE, haga clic en **Tools** >  (Herramientas) **Serial Monitor** (Monitor serie).</span><span class="sxs-lookup"><span data-stu-id="18379-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="18379-225">En la esquina inferior derecha de la ventana del monitor serie, seleccione **No line ending** (Sin final de línea) de la lista desplegable izquierda.</span><span class="sxs-lookup"><span data-stu-id="18379-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="18379-226">En la lista desplegable derecha, seleccione **115200 baud** (115 200 baudios).</span><span class="sxs-lookup"><span data-stu-id="18379-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="18379-227">En el cuadro de entrada de la parte superior, escriba la siguiente información (si se le pide que la proporcione) y haga clic en **Send** (Enviar):</span><span class="sxs-lookup"><span data-stu-id="18379-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="18379-228">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="18379-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="18379-229">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="18379-229">Wi-Fi password</span></span>
   * <span data-ttu-id="18379-230">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="18379-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="18379-231">La información de credenciales se almacena en la EEPROM de Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="18379-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="18379-232">Si hace clic en el botón de restablecimiento de la placa Feather M0 WiFi, la aplicación de ejemplo le pregunta si quiere borrar la información.</span><span class="sxs-lookup"><span data-stu-id="18379-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="18379-233">Escriba `Y` para borrar la información.</span><span class="sxs-lookup"><span data-stu-id="18379-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="18379-234">Se le pedirá que proporcione la información de nuevo.</span><span class="sxs-lookup"><span data-stu-id="18379-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="18379-235">Comprobación de que la aplicación de ejemplo se ejecuta correctamente</span><span class="sxs-lookup"><span data-stu-id="18379-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="18379-236">Si ve la siguiente salida de la ventana del monitor serie y el LED parpadea en Feather M0 WiFi, la aplicación de ejemplo se está ejecutando correctamente:</span><span class="sxs-lookup"><span data-stu-id="18379-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Salida final en el IDE de Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="18379-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="18379-238">Next steps</span></span>

<span data-ttu-id="18379-239">Ha conectado correctamente Feather M0 WiFi a IoT Hub y ha enviado los datos del sensor capturados a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="18379-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

