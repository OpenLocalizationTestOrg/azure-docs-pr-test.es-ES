---
title: "M0 toocloud: conexión Wi-Fi de desvanecimiento M0 tooAzure centro de IoT | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooset una copia de seguridad y conectarse Adafruit compacto M0 Wi-Fi tooAzure plataforma de nube de Azure de centro de IoT toosend datos toohello en este tutorial."
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
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="c0eae-103">Conectar Adafruit compacto M0 Wi-Fi tooAzure centro de IoT en nube Hola</span><span class="sxs-lookup"><span data-stu-id="c0eae-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre BME280, Feather M0 WiFi e IoT Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="c0eae-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con el panel de Arduino.</span><span class="sxs-lookup"><span data-stu-id="c0eae-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="c0eae-106">A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="c0eae-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="c0eae-107">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="c0eae-107">What you do</span></span>

<span data-ttu-id="c0eae-108">Conectar el centro de IoT de tooan Adafruit compacto M0 Wi-Fi que cree.</span><span class="sxs-lookup"><span data-stu-id="c0eae-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="c0eae-109">A continuación, ejecutar una aplicación de ejemplo en M0 Wi-Fi toocollect Hola temperatura y humedad los datos desde un BME280.</span><span class="sxs-lookup"><span data-stu-id="c0eae-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="c0eae-110">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="c0eae-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="c0eae-111">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="c0eae-111">What you learn</span></span>

* <span data-ttu-id="c0eae-112">¿Cómo toocreate un centro de IoT y registrar un dispositivo de Wi-Fi de desvanecimiento M0</span><span class="sxs-lookup"><span data-stu-id="c0eae-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="c0eae-113">¿Cómo tooconnect Wi-Fi de desvanecimiento M0 con sensor de Hola y el equipo</span><span class="sxs-lookup"><span data-stu-id="c0eae-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="c0eae-114">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en Wi-Fi de desvanecimiento M0</span><span class="sxs-lookup"><span data-stu-id="c0eae-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="c0eae-115">¿Cómo toosend Hola centro de IoT de sensor datos tooyour</span><span class="sxs-lookup"><span data-stu-id="c0eae-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c0eae-116">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="c0eae-116">What you need</span></span>

![Piezas necesarias para el tutorial de Hola](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="c0eae-118">toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de desvanecimiento M0 Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="c0eae-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="c0eae-119">Hola Wi-Fi de desvanecimiento M0 panel</span><span class="sxs-lookup"><span data-stu-id="c0eae-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="c0eae-120">Un cable USB A tooType de Micro USB</span><span class="sxs-lookup"><span data-stu-id="c0eae-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="c0eae-121">También necesita Hola después cosas para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="c0eae-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="c0eae-122">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c0eae-122">An active Azure subscription.</span></span> <span data-ttu-id="c0eae-123">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c0eae-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="c0eae-124">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c0eae-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="c0eae-125">Una red inalámbrica para Wi-Fi de desvanecimiento M0 tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="c0eae-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="c0eae-126">Una herramienta de configuración de Internet conexión toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="c0eae-127">[IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c0eae-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="c0eae-128">Las versiones anteriores no funcionan con la biblioteca de centro de IoT de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="c0eae-129">Si no dispone de un sensor, Hola siguientes elementos es opcional.</span><span class="sxs-lookup"><span data-stu-id="c0eae-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="c0eae-130">También tiene Hola opción consiste en utilizar datos de sensor simulada:</span><span class="sxs-lookup"><span data-stu-id="c0eae-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="c0eae-131">Un sensor de temperatura y humedad BME280</span><span class="sxs-lookup"><span data-stu-id="c0eae-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="c0eae-132">Una placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="c0eae-132">A breadboard</span></span>
* <span data-ttu-id="c0eae-133">Cables de puente M/M</span><span class="sxs-lookup"><span data-stu-id="c0eae-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="c0eae-134">Conexión Wi-Fi de desvanecimiento M0 con sensor Hola y el equipo</span><span class="sxs-lookup"><span data-stu-id="c0eae-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="c0eae-135">En esta sección, se conecta tooyour placa de hello sensores.</span><span class="sxs-lookup"><span data-stu-id="c0eae-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="c0eae-136">A continuación, conectar el equipo de tooyour de dispositivo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="c0eae-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="c0eae-137">Conectar un tooFeather de sensor DHT22 temperatura y humedad M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="c0eae-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="c0eae-138">Usar hello breadboard y puentes cables toomake Hola conexión.</span><span class="sxs-lookup"><span data-stu-id="c0eae-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="c0eae-139">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="c0eae-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referencia de conexiones](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="c0eae-141">Para el PIN de sensor, use Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="c0eae-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="c0eae-142">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="c0eae-142">Start (sensor)</span></span>           | <span data-ttu-id="c0eae-143">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="c0eae-143">End (board)</span></span>            | <span data-ttu-id="c0eae-144">Color del cable</span><span class="sxs-lookup"><span data-stu-id="c0eae-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="c0eae-145">VDD (patilla 27A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="c0eae-146">3V (patilla 3A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="c0eae-147">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="c0eae-147">Red cable</span></span>     |
| <span data-ttu-id="c0eae-148">GND (patilla 29A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="c0eae-149">GND (patilla 6A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="c0eae-150">Cable negro</span><span class="sxs-lookup"><span data-stu-id="c0eae-150">Black cable</span></span>   |
| <span data-ttu-id="c0eae-151">SCK (patilla 30A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="c0eae-152">SCK (patilla 12A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="c0eae-153">Cable amarillo</span><span class="sxs-lookup"><span data-stu-id="c0eae-153">Yellow cable</span></span>  |
| <span data-ttu-id="c0eae-154">SDO (patilla 31A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="c0eae-155">MI (patilla 14A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="c0eae-156">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="c0eae-156">White cable</span></span>   |
| <span data-ttu-id="c0eae-157">SDI (patilla 32A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="c0eae-158">M0 (patilla 13A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="c0eae-159">Cable azul</span><span class="sxs-lookup"><span data-stu-id="c0eae-159">Blue cable</span></span>    |
| <span data-ttu-id="c0eae-160">CS (patilla 33A)</span><span class="sxs-lookup"><span data-stu-id="c0eae-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="c0eae-161">GPIO 5 (patilla 15J)</span><span class="sxs-lookup"><span data-stu-id="c0eae-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="c0eae-162">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="c0eae-162">Orange cable</span></span>  |

<span data-ttu-id="c0eae-163">Para más información, consulte la [introducción al sensor de presión atmosférica, temperatura y humedad Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) y el artículo sobre el [patillaje de Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="c0eae-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="c0eae-164">Ahora Feather M0 WiFi debe estar conectado con un sensor en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="c0eae-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Conectar DHT22 con Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="c0eae-166">Conectar Wi-Fi de desvanecimiento M0 tooyour equipo</span><span class="sxs-lookup"><span data-stu-id="c0eae-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="c0eae-167">Usar Hola Micro USB tooType A USB cable tooconnect Wi-Fi de desvanecimiento M0 tooyour equipo, como se muestra:</span><span class="sxs-lookup"><span data-stu-id="c0eae-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Conectar compacto Huzzah tooyour equipo](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="c0eae-169">Agregar permisos de puerto serie (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="c0eae-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="c0eae-170">Si usas Ubuntu, asegúrese de que tiene Hola permisos toooperate en hello USB puerto de desvanecimiento M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c0eae-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="c0eae-171">permisos de puerto serie tooadd, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c0eae-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="c0eae-172">En un terminal, ejecute hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c0eae-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="c0eae-173">Obtener una Hola siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="c0eae-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="c0eae-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="c0eae-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="c0eae-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="c0eae-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="c0eae-176">En la salida de hello, tenga en cuenta que `uucp` o `dialout` es nombre de propietario del grupo de Hola de hello puerto USB.</span><span class="sxs-lookup"><span data-stu-id="c0eae-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="c0eae-177">tooadd hello toohello grupo de usuarios, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c0eae-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="c0eae-178">En el paso anterior de hello, obtiene el nombre de propietario del grupo de hello `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="c0eae-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="c0eae-179">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c0eae-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="c0eae-180">Para tooappear de cambio de hello, cierre la sesión de Ubuntu y, a continuación, inicie una sesión.</span><span class="sxs-lookup"><span data-stu-id="c0eae-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="c0eae-181">Recopilar datos del sensor y enviarla tooyour centro de IoT</span><span class="sxs-lookup"><span data-stu-id="c0eae-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="c0eae-182">En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="c0eae-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="c0eae-183">aplicación de ejemplo de Hola hace Hola parpadear LED en Wi-Fi de desvanecimiento M0.</span><span class="sxs-lookup"><span data-stu-id="c0eae-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="c0eae-184">A continuación, envía temperatura de Hola y recopilan los datos de humedad de hello BME280 sensor tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="c0eae-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="c0eae-185">Obtener la aplicación de ejemplo de Hola desde GitHub y preparar hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="c0eae-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="c0eae-186">aplicación de ejemplo de Hola se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0eae-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="c0eae-187">Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0eae-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="c0eae-188">repositorio de ejemplo de Hola tooclone, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c0eae-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="c0eae-189">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="c0eae-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="c0eae-190">Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.</span><span class="sxs-lookup"><span data-stu-id="c0eae-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="c0eae-191">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c0eae-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="c0eae-192">Instalar el paquete de Hola para Wi-Fi de desvanecimiento M0 Hola Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="c0eae-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="c0eae-193">Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="c0eae-194">Abra el archivo de app.ino de hello en la carpeta de la aplicación Hola Hola Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="c0eae-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Abra la aplicación de ejemplo de Hola en Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="c0eae-196">Haga clic en **archivo** > **preferencias** (Windows o Linux) o **Arduino** > **preferencias** (Mac) y copie y Pegar Hola vínculo en hello **más direcciones URL del Administrador de paneles** opción Hola preferencias Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="c0eae-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="c0eae-197">Haga clic en **herramientas** > **panel** > **paneles Manager**y, a continuación, instalar hello `Arduino SAMD Boards` versión `1.6.2` o posterior.</span><span class="sxs-lookup"><span data-stu-id="c0eae-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="c0eae-198">A continuación, en Hola la misma ventana, instale `Adafruit SAMD Boards` las definiciones de tooadd Hola panel archivo de paquete.</span><span class="sxs-lookup"><span data-stu-id="c0eae-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Hola esp8266 paquete está instalado](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="c0eae-200">Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="c0eae-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="c0eae-201">Instale los controladores (solo para Windows).</span><span class="sxs-lookup"><span data-stu-id="c0eae-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="c0eae-202">Cuando se conecta Wi-Fi de desvanecimiento M0, tendrá que tooinstall un controlador.</span><span class="sxs-lookup"><span data-stu-id="c0eae-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="c0eae-203">Haga clic en [vínculo de descarga de hello en la página Web de hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) instalador del controlador toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="c0eae-204">Siga los controladores de Hola Hola pasos tooinstall que desee.</span><span class="sxs-lookup"><span data-stu-id="c0eae-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="c0eae-205">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="c0eae-205">Install necessary libraries</span></span>

1. <span data-ttu-id="c0eae-206">Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.</span><span class="sxs-lookup"><span data-stu-id="c0eae-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="c0eae-207">Busque Hola siguiendo los nombres de las bibliotecas uno por uno.</span><span class="sxs-lookup"><span data-stu-id="c0eae-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="c0eae-208">Para cada biblioteca que encuentre, haga clic en **Install** (Instalar):</span><span class="sxs-lookup"><span data-stu-id="c0eae-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="c0eae-209">Instale manualmente `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="c0eae-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="c0eae-210">Vaya demasiado[este sitio Web](https://github.com/adafruit/Adafruit_WINC1500) y haga clic en **clon o una descarga** > **Download ZIP**.</span><span class="sxs-lookup"><span data-stu-id="c0eae-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="c0eae-211">A continuación, en el IDE Arduino, vaya demasiado**boceto** > **incluyen biblioteca** > **agregar .zip biblioteca** y agregue el archivo zip de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="c0eae-212">Usar la aplicación de ejemplo de Hola si no tienes un sensor BME280 real</span><span class="sxs-lookup"><span data-stu-id="c0eae-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="c0eae-213">Si no dispone de un sensor BME280 real, aplicación de ejemplo de Hola puede simular los datos de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="c0eae-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="c0eae-214">tooset los datos de toouse simulado de aplicación de ejemplo Hola, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c0eae-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="c0eae-215">Abra hello `config.h` archivo Hola `app` carpeta.</span><span class="sxs-lookup"><span data-stu-id="c0eae-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="c0eae-216">Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="c0eae-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="c0eae-218">Guardar archivo de hello con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="c0eae-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="c0eae-219">Implementar tooFeather de aplicación de ejemplo de Hola M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="c0eae-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="c0eae-220">Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola de Wi-Fi de desvanecimiento M0.</span><span class="sxs-lookup"><span data-stu-id="c0eae-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="c0eae-221">Haga clic en **boceto** > **cargar** toobuild e implementar tooFeather de aplicación de ejemplo de Hola M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c0eae-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="c0eae-222">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="c0eae-222">Enter your credentials</span></span>

<span data-ttu-id="c0eae-223">Una vez finalizada correctamente la carga de hello, siga estos pasos tooenter sus credenciales:</span><span class="sxs-lookup"><span data-stu-id="c0eae-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="c0eae-224">Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.</span><span class="sxs-lookup"><span data-stu-id="c0eae-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="c0eae-225">En la esquina inferior derecha de saludo de la ventana del monitor de la serie de hello, seleccione **ningún final de línea** en lista de desplegable Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="c0eae-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="c0eae-226">Seleccione **115.200 baudios** en lista desplegable Hola Hola derecho.</span><span class="sxs-lookup"><span data-stu-id="c0eae-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="c0eae-227">En el cuadro de entrada de hello en la parte superior de hello, escriba Hola siguiente información si le pide tooprovide y haga clic en **enviar**:</span><span class="sxs-lookup"><span data-stu-id="c0eae-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="c0eae-228">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="c0eae-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="c0eae-229">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="c0eae-229">Wi-Fi password</span></span>
   * <span data-ttu-id="c0eae-230">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="c0eae-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="c0eae-231">información de credenciales de Hola se almacena en hello EEPROM de desvanecimiento M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c0eae-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="c0eae-232">Si hace clic en botón de reinicio de hello en hello placa de Wi-Fi de desvanecimiento M0, aplicación de ejemplo de Hola le preguntará si desea que tooerase información de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0eae-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="c0eae-233">Escriba `Y` información de hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="c0eae-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="c0eae-234">Se le pide información de hello tooprovide una segunda vez.</span><span class="sxs-lookup"><span data-stu-id="c0eae-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="c0eae-235">Compruebe que la aplicación de ejemplo de Hola se ejecuta correctamente</span><span class="sxs-lookup"><span data-stu-id="c0eae-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="c0eae-236">Si ve siguiente Hola de salida de ventana del monitor de la serie de Hola y Hola parpadear LED de desvanecimiento M0 Wi-Fi, aplicación de ejemplo de Hola se esté ejecutando correctamente:</span><span class="sxs-lookup"><span data-stu-id="c0eae-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Salida final en el IDE de Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="c0eae-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c0eae-238">Next steps</span></span>

<span data-ttu-id="c0eae-239">Está correctamente conectado centro de IoT de Wi-Fi de desvanecimiento M0 tooyour y envía el centro de IoT de hello capturan sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="c0eae-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

