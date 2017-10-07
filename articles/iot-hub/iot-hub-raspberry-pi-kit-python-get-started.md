---
title: aaaRaspberry Pi toocloud (Python) - conectar frambuesa Pi tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse frambuesa Pi tooAzure centro de IoT para la plataforma de nube de Azure de frambuesa Pi toosend datos toohello en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot frambuesas pi, frambuesas pi iot hub, frambuesas pi envío datos toocloud, frambuesas pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="b51a9-104">Conectar frambuesa Pi tooAzure centro de IoT (Python)</span><span class="sxs-lookup"><span data-stu-id="b51a9-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="b51a9-105">En este tutorial, empiece por obtener información sobre fundamentos de hello sobre cómo trabajar con frambuesa Pi que se está ejecutando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="b51a9-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="b51a9-106">A continuación, aprenderá cómo tooseamlessly conectar la nube de toohello de dispositivos mediante el uso de [centro de IoT de Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="b51a9-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="b51a9-107">Para obtener ejemplos de Windows 10 IoT Core, vaya toohello [centro de desarrollo de Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="b51a9-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="b51a9-108">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="b51a9-108">Don't have a kit yet?</span></span> <span data-ttu-id="b51a9-109">Pruebe el [simulador en línea de Rapsberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b51a9-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="b51a9-110">También puede comprar un nuevo kit [aquí](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="b51a9-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b51a9-111">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="b51a9-111">What you do</span></span>

* <span data-ttu-id="b51a9-112">Cree un Centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b51a9-112">Create an IoT hub.</span></span>
* <span data-ttu-id="b51a9-113">Registre un dispositivo para Pi en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b51a9-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="b51a9-114">Configure Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="b51a9-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="b51a9-115">Ejecutar una aplicación de ejemplo en el centro de IoT de Pi toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b51a9-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="b51a9-116">Conectar el centro de IoT de frambuesa Pi tooan creados por usted.</span><span class="sxs-lookup"><span data-stu-id="b51a9-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="b51a9-117">A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect Pi de un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="b51a9-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="b51a9-118">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b51a9-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b51a9-119">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="b51a9-119">What you learn</span></span>

* <span data-ttu-id="b51a9-120">¿Cómo toocreate un centro de IoT de Azure y obtener la cadena de conexión de dispositivo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b51a9-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="b51a9-121">¿Cómo tooconnect Pi con un sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="b51a9-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="b51a9-122">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo de Pi.</span><span class="sxs-lookup"><span data-stu-id="b51a9-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="b51a9-123">Cómo centro de IoT de toosend sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b51a9-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b51a9-124">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="b51a9-124">What you need</span></span>

![Lo que necesita](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="b51a9-126">Hola frambuesa Pi 2 o 3 de Pi de frambuesa al panel.</span><span class="sxs-lookup"><span data-stu-id="b51a9-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="b51a9-127">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b51a9-127">An active Azure subscription.</span></span> <span data-ttu-id="b51a9-128">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b51a9-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b51a9-129">Un monitor, un teclado USB y mouse (ratón) que se conectan tooPi.</span><span class="sxs-lookup"><span data-stu-id="b51a9-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="b51a9-130">Un equipo PC o Mac con Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="b51a9-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="b51a9-131">Una conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="b51a9-131">An Internet connection.</span></span>
* <span data-ttu-id="b51a9-132">Una tarjeta microSD de 16 GB o más.</span><span class="sxs-lookup"><span data-stu-id="b51a9-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="b51a9-133">Un SD USB adaptador o microSD tarjeta tooburn Hola imagen de sistema operativo en tarjeta microSD de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="b51a9-134">Alimentación de amp 2 de 5 voltios con cable de hello pie 6 micro USB.</span><span class="sxs-lookup"><span data-stu-id="b51a9-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="b51a9-135">Hola siguientes elementos es opcional:</span><span class="sxs-lookup"><span data-stu-id="b51a9-135">hello following items are optional:</span></span>

* <span data-ttu-id="b51a9-136">Un sensor de temperatura, presión y humedad Adafruit BME280 ensamblado.</span><span class="sxs-lookup"><span data-stu-id="b51a9-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="b51a9-137">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="b51a9-137">A breadboard.</span></span>
* <span data-ttu-id="b51a9-138">Cables de puente M/6 F.</span><span class="sxs-lookup"><span data-stu-id="b51a9-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="b51a9-139">Un LED difuso de 10 mm.</span><span class="sxs-lookup"><span data-stu-id="b51a9-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="b51a9-140">Estos elementos son opcionales, porque la compatibilidad de ejemplo de código de hello había simulado los datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="b51a9-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="b51a9-141">Configuración de Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="b51a9-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="b51a9-142">Instalar el sistema operativo de hello Raspbian de Pi</span><span class="sxs-lookup"><span data-stu-id="b51a9-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="b51a9-143">Preparar la tarjeta microSD de hello para la instalación de la imagen de Raspbian Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="b51a9-144">Descargue Raspbian.</span><span class="sxs-lookup"><span data-stu-id="b51a9-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="b51a9-145">[Descargar Raspbian Jessie con el escritorio](https://www.raspberrypi.org/downloads/raspbian/) (archivo .zip de hello).</span><span class="sxs-lookup"><span data-stu-id="b51a9-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="b51a9-146">Extraer hello Raspbian imagen tooa carpeta del equipo.</span><span class="sxs-lookup"><span data-stu-id="b51a9-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="b51a9-147">Instalar Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b51a9-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="b51a9-148">[Descargar e instalar la utilidad de grabadora de tarjeta de SD de creación de hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="b51a9-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="b51a9-149">Ejecute creación y seleccione la imagen de Raspbian Hola que ha extraído en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="b51a9-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="b51a9-150">Seleccione la unidad de tarjeta microSD Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-150">Select hello microSD card drive.</span></span> <span data-ttu-id="b51a9-151">Tenga en cuenta que creación probablemente ya seleccionó unidad correcta Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="b51a9-152">Haga clic en Flash tooinstall Raspbian toohello microSD tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b51a9-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="b51a9-153">Quitar tarjeta microSD de hello del equipo cuando se completa la instalación.</span><span class="sxs-lookup"><span data-stu-id="b51a9-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="b51a9-154">Es tarjeta microSD de tooremove seguro Hola directamente porque creación expulsa automáticamente o desmonta tarjeta microSD de hello tras la finalización.</span><span class="sxs-lookup"><span data-stu-id="b51a9-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="b51a9-155">Inserte la tarjeta microSD de hello en Pi.</span><span class="sxs-lookup"><span data-stu-id="b51a9-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="b51a9-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="b51a9-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="b51a9-157">Conecte el monitor de toohello de Pi, teclado y mouse (ratón), inicie Pi y, a continuación, inicie sesión en Raspbian con `pi` como nombre de usuario de Hola y `raspberry` como contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="b51a9-158">Haga clic en icono frambuesas hello > **preferencias** > **frambuesa Pi configuración**.</span><span class="sxs-lookup"><span data-stu-id="b51a9-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menú de Hello Raspbian preferencias](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="b51a9-160">En hello **Interfaces** pestaña, establezca **I2C** y **SSH** demasiado**habilitar**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b51a9-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="b51a9-161">Si no tiene sensores físicos y desea que los datos de sensor toouse simulado, este paso es opcional.</span><span class="sxs-lookup"><span data-stu-id="b51a9-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C y SSH en Raspberry Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="b51a9-163">tooenable SSH y I2C, puede encontrar varios documentos de referencia en [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) y [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="b51a9-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="b51a9-164">Conectar Hola sensor tooPi</span><span class="sxs-lookup"><span data-stu-id="b51a9-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="b51a9-165">Utilice hello breadboard y puentes cables tooconnect un LED y un tooPi BME280 como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="b51a9-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="b51a9-166">Si no dispone de sensor hello, [omitir esta sección](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="b51a9-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Hola frambuesa Pi y sensor de conexión](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="b51a9-168">sensor de Hello BME280 puede recopilar datos de temperatura y humedad.</span><span class="sxs-lookup"><span data-stu-id="b51a9-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="b51a9-169">Y Hola LED parpadea si se produce una comunicación entre el dispositivo y hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="b51a9-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="b51a9-170">Para el PIN de sensor, use Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="b51a9-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="b51a9-171">Inicio (sensor y LED)</span><span class="sxs-lookup"><span data-stu-id="b51a9-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="b51a9-172">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="b51a9-172">End (Board)</span></span>            | <span data-ttu-id="b51a9-173">Color de cable</span><span class="sxs-lookup"><span data-stu-id="b51a9-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b51a9-174">VDD (patilla 5G)</span><span class="sxs-lookup"><span data-stu-id="b51a9-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="b51a9-175">Potencia 3,3 V (patilla 1)</span><span class="sxs-lookup"><span data-stu-id="b51a9-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="b51a9-176">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="b51a9-176">White cable</span></span>   |
| <span data-ttu-id="b51a9-177">GND (patilla 7G)</span><span class="sxs-lookup"><span data-stu-id="b51a9-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="b51a9-178">GND (patilla 6)</span><span class="sxs-lookup"><span data-stu-id="b51a9-178">GND (Pin 6)</span></span>            | <span data-ttu-id="b51a9-179">Cable marrón</span><span class="sxs-lookup"><span data-stu-id="b51a9-179">Brown cable</span></span>   |
| <span data-ttu-id="b51a9-180">SDI (patilla 10G)</span><span class="sxs-lookup"><span data-stu-id="b51a9-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="b51a9-181">I2C1 SDA (patilla 3)</span><span class="sxs-lookup"><span data-stu-id="b51a9-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="b51a9-182">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="b51a9-182">Red cable</span></span>     |
| <span data-ttu-id="b51a9-183">SCK (patilla 8G)</span><span class="sxs-lookup"><span data-stu-id="b51a9-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="b51a9-184">I2C1 SCL (patilla 5)</span><span class="sxs-lookup"><span data-stu-id="b51a9-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="b51a9-185">Cable naranja</span><span class="sxs-lookup"><span data-stu-id="b51a9-185">Orange cable</span></span>  |
| <span data-ttu-id="b51a9-186">LED VDD (patilla 18F)</span><span class="sxs-lookup"><span data-stu-id="b51a9-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="b51a9-187">GPIO 24 (patilla 18)</span><span class="sxs-lookup"><span data-stu-id="b51a9-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="b51a9-188">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="b51a9-188">White cable</span></span>   |
| <span data-ttu-id="b51a9-189">LED GND (patilla 17F)</span><span class="sxs-lookup"><span data-stu-id="b51a9-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="b51a9-190">GND (patilla 20)</span><span class="sxs-lookup"><span data-stu-id="b51a9-190">GND (Pin 20)</span></span>           | <span data-ttu-id="b51a9-191">Cable negro</span><span class="sxs-lookup"><span data-stu-id="b51a9-191">Black cable</span></span>   |

<span data-ttu-id="b51a9-192">Haga clic en tooview [frambuesa Pi 2 y 3 asignaciones de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para su referencia.</span><span class="sxs-lookup"><span data-stu-id="b51a9-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="b51a9-193">Una vez se haya conectado correctamente BME280 tooyour frambuesa Pi, debería ser como debajo de imagen.</span><span class="sxs-lookup"><span data-stu-id="b51a9-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi y BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="b51a9-195">Conectar red toohello de Pi</span><span class="sxs-lookup"><span data-stu-id="b51a9-195">Connect Pi toohello network</span></span>

<span data-ttu-id="b51a9-196">Activar Pi mediante cable USB micro de Hola y fuente de alimentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="b51a9-197">Use Hola Ethernet por cable tooconnect Pi tooyour con cable de red o siga hello [las instrucciones de hello frambuesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) red inalámbrica de tooconnect Pi tooyour.</span><span class="sxs-lookup"><span data-stu-id="b51a9-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="b51a9-198">Después de que el instalador de plataforma ha sido red toohello conectado correctamente, deberá tootake una nota de hello [dirección IP de su Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="b51a9-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Red toowired conectado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="b51a9-200">Asegúrese de que ese Pi está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="b51a9-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="b51a9-201">Por ejemplo, si el equipo está conectado tooa red inalámbrica mientras Pi es tooa conectado por cable de red, no verá Hola IP dirección en la salida de hello devdisco.</span><span class="sxs-lookup"><span data-stu-id="b51a9-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="b51a9-202">Ejecutar una aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="b51a9-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="b51a9-203">Instalar paquetes de requisitos previos de Hola</span><span class="sxs-lookup"><span data-stu-id="b51a9-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="b51a9-204">Utilice uno de hello siguiendo a los clientes SSH de su tooyour de tooconnect del equipo host frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="b51a9-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="b51a9-205">**Usuarios de Windows**</span><span class="sxs-lookup"><span data-stu-id="b51a9-205">**Windows Users**</span></span>
   1. <span data-ttu-id="b51a9-206">Descargue e instale [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="b51a9-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="b51a9-207">Copie la dirección IP de saludo de la sección de Pi en nombre de Host de hello (o dirección IP) y seleccione SSH como tipo de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="b51a9-208">**Usuarios de Mac y Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b51a9-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="b51a9-209">Use el cliente SSH integrado de hello en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="b51a9-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="b51a9-210">Es posible que tenga toorun `ssh pi@<ip address of pi>` tooconnect Pi mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="b51a9-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="b51a9-211">el nombre de usuario de Hello predeterminada es `pi` , y es la contraseña de hello `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="b51a9-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="b51a9-212">Configurar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b51a9-212">Configure hello sample application</span></span>

1. <span data-ttu-id="b51a9-213">Clonar aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b51a9-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="b51a9-214">Abra el archivo de configuración de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="b51a9-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="b51a9-215">Hay cinco macros en este archivo que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="b51a9-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="b51a9-216">Hello primero uno es `MESSAGE_TIMESPAN`, que define el intervalo de tiempo de hello (en milisegundos) entre los dos mensajes que envían toocloud.</span><span class="sxs-lookup"><span data-stu-id="b51a9-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="b51a9-217">Hola otra `SIMULATED_DATA`, que es un valor booleano para si toouse simulado los datos de sensor o no.</span><span class="sxs-lookup"><span data-stu-id="b51a9-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="b51a9-218">`I2C_ADDRESS`es la dirección de hello I2C que está conectado el sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="b51a9-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="b51a9-219">`GPIO_PIN_ADDRESS`es la dirección GPIO de hello para el LED.</span><span class="sxs-lookup"><span data-stu-id="b51a9-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="b51a9-220">Hello en último lugar uno es `BLINK_TIMESPAN`, que define el intervalo de tiempo de hello cuando se activa el LED en milisegundos.</span><span class="sxs-lookup"><span data-stu-id="b51a9-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="b51a9-221">Si se **no tiene el sensor de hello**, hello establezca `SIMULATED_DATA` valor demasiado`True` aplicación de ejemplo de Hola toomake crear y utilizar datos de detección simulada.</span><span class="sxs-lookup"><span data-stu-id="b51a9-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="b51a9-222">Guarde y salga al presionar Control-O > Entrar > Control-X.</span><span class="sxs-lookup"><span data-stu-id="b51a9-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="b51a9-223">Compilar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b51a9-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="b51a9-224">Compile la aplicación de ejemplo de Hola ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="b51a9-225">Como hello Azure IoT SDK para Python son contenedores que funcionan sobre Hola SDK de C de dispositivos de IoT de Azure, necesitará bibliotecas de hello C toocompile si desea o necesita bibliotecas de Python toogenerate Hola desde el código fuente.</span><span class="sxs-lookup"><span data-stu-id="b51a9-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="b51a9-226">También puede especificar la versión de Hola que desee mediante la ejecución de `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="b51a9-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="b51a9-227">Si ejecuta el script sin el parámetro, el script de Hola detectará automáticamente versión Hola de python instalado (secuencia de búsqueda 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="b51a9-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="b51a9-228">Asegúrese de que su versión de Python mantenga la coherencia durante la compilación y la ejecución.</span><span class="sxs-lookup"><span data-stu-id="b51a9-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="b51a9-229">En la creación de biblioteca de cliente de Python de hello (iothub_client.so) en dispositivos de Linux que tienen menos de 1GB de RAM, verá compilar acumulando en 98% durante la creación de iothub_client_python.cpp tal y como se muestra a continuación `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="b51a9-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="b51a9-230">Si experimenta este problema, compruebe el consumo de memoria de hello de dispositivo de hello mediante `free -m command` en otra ventana de terminal durante ese tiempo.</span><span class="sxs-lookup"><span data-stu-id="b51a9-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="b51a9-231">Si se está quedando sin memoria mientras se estaba compilando el archivo iothub_client_python.cpp, puede que tenga tootemporarily aumentar tooget de espacio de intercambio de hello toosuccessfully de memoria insuficiente compilar biblioteca del SDK de dispositivo de Hola de cliente de Python.</span><span class="sxs-lookup"><span data-stu-id="b51a9-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="b51a9-232">Ejecute la aplicación de ejemplo de Hola con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b51a9-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="b51a9-233">Asegúrese de que copia y pegar cadena de conexión de dispositivo de hello en comillas simples de Hola.</span><span class="sxs-lookup"><span data-stu-id="b51a9-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="b51a9-234">Y si usar python Hola 3, puede usar Hola comando `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="b51a9-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="b51a9-235">Debería ver la siguiente Hola de salida que muestra Hola mensajes hello y datos del sensor que se envían tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b51a9-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Salida: datos de sensor enviados desde el centro de IoT de frambuesa Pi tooyour](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="b51a9-237">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b51a9-237">Next steps</span></span>

<span data-ttu-id="b51a9-238">Se han ejecutado un datos de sensor de toocollect de aplicación de ejemplo y se envía tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b51a9-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="b51a9-239">mensajes de saludo de toosee que el instalador de plataforma de frambuesa ha enviado IoT de tooyour concentrador o envío tooyour de mensajes frambuesa Pi en una interfaz de línea de comandos, vea hello [administrar nube dispositivo mensajería con el centro de IOT explorer, tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="b51a9-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
