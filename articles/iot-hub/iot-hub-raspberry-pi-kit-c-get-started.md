---
title: aaaRaspberry Pi toocloud (C) - conectar frambuesa Pi tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse frambuesa Pi tooAzure centro de IoT para la plataforma de nube de Azure de frambuesa Pi toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot frambuesas pi, frambuesas pi iot hub, frambuesas pi envío datos toocloud, frambuesas pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="ce0af-104">Conectar frambuesa Pi tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="ce0af-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="ce0af-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con frambuesa Pi que se está ejecutando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="ce0af-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="ce0af-106">A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="ce0af-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="ce0af-107">Para obtener ejemplos de Windows 10 IoT Core, vaya toohello [centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="ce0af-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="ce0af-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="ce0af-108">Don't have a kit yet?</span></span> <span data-ttu-id="ce0af-109">Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce0af-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="ce0af-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="ce0af-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ce0af-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="ce0af-111">What you do</span></span>

* <span data-ttu-id="ce0af-112">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ce0af-112">Create an IoT hub.</span></span>
* <span data-ttu-id="ce0af-113">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ce0af-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="ce0af-114">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="ce0af-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="ce0af-115">Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce0af-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="ce0af-116">Conectar el centro de IoT de frambuesa Pi tooan creados por usted.</span><span class="sxs-lookup"><span data-stu-id="ce0af-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="ce0af-117">A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect Pi de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="ce0af-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="ce0af-118">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce0af-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ce0af-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="ce0af-119">What you learn</span></span>

* <span data-ttu-id="ce0af-120">¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ce0af-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="ce0af-121">¿Cómo tooconnect Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="ce0af-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="ce0af-122">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo de Pi.</span><span class="sxs-lookup"><span data-stu-id="ce0af-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="ce0af-123">Cómo centro de IoT de toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce0af-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ce0af-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="ce0af-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="ce0af-126">Hola frambuesa Pi 2 o 3 de Pi de frambuesa al panel.</span><span class="sxs-lookup"><span data-stu-id="ce0af-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="ce0af-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ce0af-127">An active Azure subscription.</span></span> <span data-ttu-id="ce0af-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="ce0af-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ce0af-129">Un monitor, un teclado USB y mouse (ratón) que se conectan tooPi.</span><span class="sxs-lookup"><span data-stu-id="ce0af-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="ce0af-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="ce0af-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="ce0af-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="ce0af-131">An Internet connection.</span></span>
* <span data-ttu-id="ce0af-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="ce0af-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="ce0af-133">Un SD USB adaptador o microSD tarjeta tooburn Hola imagen de sistema operativo en tarjeta microSD de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="ce0af-134">Alimentación de amp 2 de 5 voltios con cable de hello pie 6 micro USB.</span><span class="sxs-lookup"><span data-stu-id="ce0af-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="ce0af-135">Hola siguientes elementos es opcional:</span><span class="sxs-lookup"><span data-stu-id="ce0af-135">hello following items are optional:</span></span>

* <span data-ttu-id="ce0af-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="ce0af-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="ce0af-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="ce0af-137">A breadboard.</span></span>
* <span data-ttu-id="ce0af-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="ce0af-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="ce0af-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="ce0af-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="ce0af-140">Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="ce0af-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="ce0af-141">Configurar Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="ce0af-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="ce0af-142">Instalar el sistema operativo de hello Raspbian de Pi</span><span class="sxs-lookup"><span data-stu-id="ce0af-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="ce0af-143">Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="ce0af-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="ce0af-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="ce0af-145">[Descargar Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (archivo .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="ce0af-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="ce0af-146">Extraer hello Raspbian imagen tooa carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="ce0af-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="ce0af-147">Instalar Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ce0af-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="ce0af-148">[Descargar e instalar la utilidad de grabadora de tarjeta de SD de creación de hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="ce0af-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="ce0af-149">Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="ce0af-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="ce0af-150">Seleccione la unidad de tarjeta microSD Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-150">Select hello microSD card drive.</span></span> <span data-ttu-id="ce0af-151">Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="ce0af-152">Haga clic en Flash tooinstall Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="ce0af-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="ce0af-153">Quitar tarjeta microSD de hello del equipo cuando se completa la instalación.</span><span class="sxs-lookup"><span data-stu-id="ce0af-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="ce0af-154">Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.</span><span class="sxs-lookup"><span data-stu-id="ce0af-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="ce0af-155">Inserte la tarjeta microSD de hello en Pi.</span><span class="sxs-lookup"><span data-stu-id="ce0af-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="ce0af-156">Habilitar SSH y SPI</span><span class="sxs-lookup"><span data-stu-id="ce0af-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="ce0af-157">Conecte el monitor de toohello de Pi, teclado y mouse (ratón), inicie Pi y, a continuación, inicie sesión en Raspbian con `pi` como nombre de usuario de Hola y `raspberry` como contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="ce0af-158">Haga clic en icono frambuesas hello > **preferencias** > **frambuesa Pi configuración**.</span><span class="sxs-lookup"><span data-stu-id="ce0af-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menú de Hello Raspbian preferencias](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="ce0af-160">En hello **Interfaces** pestaña, establezca **SPI** y **SSH** demasiado**habilitar**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ce0af-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="ce0af-161">Si no tiene sensores físicos y desea que los datos de sensor toouse simulado, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="ce0af-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Habilitar SPI y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="ce0af-163">tooenable SSH y SPI, puede encontrar varios documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="ce0af-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="ce0af-164">Conectar Hola sensor tooPi</span><span class="sxs-lookup"><span data-stu-id="ce0af-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="ce0af-165">Utilice hello breadboard y puentes cables tooconnect un LED y un tooPi BME280 como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="ce0af-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="ce0af-166">Si no dispone de sensor hello, [omitir esta sección](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="ce0af-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hola frambuesa Pi y sensor de conexión](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="ce0af-168">sensor de Hello BME280 puede recopilar datos de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="ce0af-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="ce0af-169">Y Hola LED parpadea si se produce una comunicación entre el dispositivo y hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="ce0af-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="ce0af-170">Para el PIN de sensor, use Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="ce0af-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="ce0af-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="ce0af-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="ce0af-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="ce0af-172">End (Board)</span></span>            | <span data-ttu-id="ce0af-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="ce0af-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="ce0af-174">LED VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="ce0af-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="ce0af-175">GPIO 4 (patilla 7)</span><span class="sxs-lookup"><span data-stu-id="ce0af-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="ce0af-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="ce0af-176">White cable</span></span>   |
| <span data-ttu-id="ce0af-177">LED GND (patilla 6G)</span><span class="sxs-lookup"><span data-stu-id="ce0af-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="ce0af-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="ce0af-178">GND (Pin 6)</span></span>            | <span data-ttu-id="ce0af-179">Cable negro</span><span class="sxs-lookup"><span data-stu-id="ce0af-179">Black cable</span></span>   |
| <span data-ttu-id="ce0af-180">VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="ce0af-181">Potencia 3,3 V (patilla 17)</span><span class="sxs-lookup"><span data-stu-id="ce0af-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="ce0af-182">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="ce0af-182">White cable</span></span>   |
| <span data-ttu-id="ce0af-183">GND (patilla 20F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="ce0af-184">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="ce0af-184">GND (Pin 20)</span></span>           | <span data-ttu-id="ce0af-185">Cable negro</span><span class="sxs-lookup"><span data-stu-id="ce0af-185">Black cable</span></span>   |
| <span data-ttu-id="ce0af-186">SCK (patilla 21F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="ce0af-187">SPI0 SCLK (patilla 23)</span><span class="sxs-lookup"><span data-stu-id="ce0af-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="ce0af-188">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="ce0af-188">Orange cable</span></span>  |
| <span data-ttu-id="ce0af-189">SDO (patilla 22F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="ce0af-190">SPI0 MISO (patilla 21)</span><span class="sxs-lookup"><span data-stu-id="ce0af-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="ce0af-191">Cable amarillo</span><span class="sxs-lookup"><span data-stu-id="ce0af-191">Yellow cable</span></span>  |
| <span data-ttu-id="ce0af-192">SDI (patilla 23F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="ce0af-193">SPI0 MOSI (patilla 19)</span><span class="sxs-lookup"><span data-stu-id="ce0af-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="ce0af-194">Cable verde</span><span class="sxs-lookup"><span data-stu-id="ce0af-194">Green cable</span></span>   |
| <span data-ttu-id="ce0af-195">CS (patilla 24F)</span><span class="sxs-lookup"><span data-stu-id="ce0af-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="ce0af-196">SPI0 CS (patilla 24)</span><span class="sxs-lookup"><span data-stu-id="ce0af-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="ce0af-197">Cable azul</span><span class="sxs-lookup"><span data-stu-id="ce0af-197">Blue cable</span></span>    |

<span data-ttu-id="ce0af-198">Haga clic en tooview [frambuesa Pi 2 y 3 asignaciones de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="ce0af-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="ce0af-199">Una vez se haya conectado correctamente BME280 tooyour frambuesa Pi, debería ser como debajo de imagen.</span><span class="sxs-lookup"><span data-stu-id="ce0af-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="ce0af-201">Conectar red toohello de Pi</span><span class="sxs-lookup"><span data-stu-id="ce0af-201">Connect Pi toohello network</span></span>

<span data-ttu-id="ce0af-202">Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="ce0af-203">Use Hola Ethernet por cable tooconnect Pi tooyour con cable de red o siga hello [las instrucciones de hello frambuesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) red inalámbrica de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce0af-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="ce0af-204">Después de que el instalador de plataforma ha sido red toohello conectado correctamente, deberá tootake una nota de hello [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="ce0af-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Red toowired conectado](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="ce0af-206">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="ce0af-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="ce0af-207">Instalar paquetes de requisitos previos de Hola</span><span class="sxs-lookup"><span data-stu-id="ce0af-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="ce0af-208">Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="ce0af-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="ce0af-209">**Usuarios de Windows**</span><span class="sxs-lookup"><span data-stu-id="ce0af-209">**Windows Users**</span></span>
   1. <span data-ttu-id="ce0af-210">Descargue e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="ce0af-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="ce0af-211">Copie la dirección IP de saludo de la sección de Pi en nombre de Host de hello (o dirección IP) y seleccione SSH como tipo de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="ce0af-213">**Usuarios de Mac y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="ce0af-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="ce0af-214">Use el cliente SSH integrado de hello en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="ce0af-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="ce0af-215">Es posible que tenga toorun `ssh pi@<ip address of pi>` tooconnect Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="ce0af-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="ce0af-216">el nombre de usuario de Hello predeterminada es `pi` , y es la contraseña de hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="ce0af-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="ce0af-217">Instalar paquetes de requisitos previos de Hola para hello SDK de dispositivos de IoT de Azure de Microsoft para C y Cmake ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ce0af-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

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


### <a name="configure-hello-sample-application"></a><span data-ttu-id="ce0af-218">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="ce0af-218">Configure hello sample application</span></span>

1. <span data-ttu-id="ce0af-219">Clonar aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ce0af-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="ce0af-220">Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="ce0af-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Archivo config](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="ce0af-222">Hay dos macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="ce0af-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="ce0af-223">Hello primero uno es `INTERVAL`, que define el intervalo de tiempo de hello (en milisegundos) entre los dos mensajes que envían toocloud.</span><span class="sxs-lookup"><span data-stu-id="ce0af-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="ce0af-224">Hola otra `SIMULATED_DATA`, que es un valor booleano para si toouse simulado los datos de sensor o no.</span><span class="sxs-lookup"><span data-stu-id="ce0af-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="ce0af-225">Si se **no tiene el sensor de hello**, hello establezca `SIMULATED_DATA` valor demasiado`1` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.</span><span class="sxs-lookup"><span data-stu-id="ce0af-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="ce0af-226">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="ce0af-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="ce0af-227">Compilar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="ce0af-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="ce0af-228">Crear aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ce0af-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Resultado de la compilación](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="ce0af-230">Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ce0af-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="ce0af-231">Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce0af-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="ce0af-232">Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ce0af-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="ce0af-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce0af-234">Next steps</span></span>

<span data-ttu-id="ce0af-235">Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="ce0af-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="ce0af-236">mensajes de saludo de toosee que el instalador de plataforma de frambuesa ha enviado IoT de tooyour concentrador o envío tooyour de mensajes frambuesa Pi en una interfaz de línea de comandos, vea hello [administrar nube dispositivo mensajería con el centro de IOT explorer, tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="ce0af-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
