---
title: aaaESP8266 toocloud - conectar Sparkfun ESP8266 lo Dev tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conectarse de plataforma de nube de Azure de toosend datos toohello Sparkfun ESP8266 lo Dev tooAzure centro de IoT para ella en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="89544-103">Conectar Sparkfun ESP8266 lo Dev tooAzure centro de IoT en nube Hola</span><span class="sxs-lookup"><span data-stu-id="89544-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexión entre DHT22, Thing Dev, y IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="89544-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="89544-105">What you will do</span></span>

<span data-ttu-id="89544-106">Conectar el centro de IoT tooan de desarrollo de Sparkfun ESP8266 lo que creará.</span><span class="sxs-lookup"><span data-stu-id="89544-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="89544-107">A continuación, ejecutar una aplicación de ejemplo en los datos de temperatura y humedad toocollect ESP8266 desde un sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="89544-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="89544-108">Por último, envíe el centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="89544-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="89544-109">Si usa otros paneles ESP8266, aún puede seguir estos pasos tooconnect, centro de IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="89544-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="89544-110">Dependiendo de la placa de hello ESP8266 que está utilizando, puede que necesite tooreconfigure Hola `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="89544-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="89544-111">Por ejemplo, si usas ESP8266 desde Pensador AI, puede cambiarlo de `0` demasiado`2`.</span><span class="sxs-lookup"><span data-stu-id="89544-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="89544-112">¿Aún no tiene el kit?, haga clic [aquí](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="89544-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="89544-113">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="89544-113">What you will learn</span></span>

* <span data-ttu-id="89544-114">¿Cómo toocreate un centro de IoT y registrar un dispositivo para algo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="89544-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="89544-115">¿Cómo tooconnect lo desarrollo con sensor de Hola y el equipo.</span><span class="sxs-lookup"><span data-stu-id="89544-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="89544-116">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en algo de desarrollo</span><span class="sxs-lookup"><span data-stu-id="89544-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="89544-117">¿Cómo toosend Hola centro de IoT de tooyour de datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="89544-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="89544-118">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="89544-118">What you will need</span></span>

![Piezas necesarias para el tutorial de Hola](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="89544-120">toocomplete esta operación, necesita Hola siguientes partes de los Starter Kit de desarrollo de lo:</span><span class="sxs-lookup"><span data-stu-id="89544-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="89544-121">Hola Sparkfun ESP8266 lo Dev panel.</span><span class="sxs-lookup"><span data-stu-id="89544-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="89544-122">Un cable USB A Micro USB tooType.</span><span class="sxs-lookup"><span data-stu-id="89544-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="89544-123">También necesita Hola siguiente para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="89544-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="89544-124">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="89544-124">An active Azure subscription.</span></span> <span data-ttu-id="89544-125">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="89544-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="89544-126">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="89544-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="89544-127">Red inalámbrica para tooconnect Sparkfun ESP8266 lo Dev a.</span><span class="sxs-lookup"><span data-stu-id="89544-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="89544-128">Herramienta de configuración de Hola de toodownload de la conexión de Internet.</span><span class="sxs-lookup"><span data-stu-id="89544-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="89544-129">[Arduino IDE](https://www.arduino.cc/en/main/software) versión 1.6.8 (o posterior), las versiones anteriores no funcionarán con la biblioteca de AzureIoT Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="89544-130">Hello elementos siguientes son opcionales en caso de que no tiene un sensor.</span><span class="sxs-lookup"><span data-stu-id="89544-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="89544-131">También tiene Hola opción consiste en utilizar datos de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="89544-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="89544-132">Un sensor de temperatura y humedad Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="89544-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="89544-133">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="89544-133">A breadboard.</span></span>
* <span data-ttu-id="89544-134">Cables de puente M/M.</span><span class="sxs-lookup"><span data-stu-id="89544-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="89544-135">Conectar ESP8266 lo desarrollo con sensor de Hola y el equipo</span><span class="sxs-lookup"><span data-stu-id="89544-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="89544-136">Conectar un sensor de temperatura y humedad DHT22 tooESP8266 lo desarrollo</span><span class="sxs-lookup"><span data-stu-id="89544-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="89544-137">Utilice hello breadboard y puentes cables toomake Hola conexión como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="89544-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="89544-138">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="89544-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![referencia de conexiones](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="89544-140">Para el PIN de sensor, usaremos Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="89544-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="89544-141">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="89544-141">Start (Sensor)</span></span>           | <span data-ttu-id="89544-142">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="89544-142">End (Board)</span></span>           | <span data-ttu-id="89544-143">Color de cable</span><span class="sxs-lookup"><span data-stu-id="89544-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="89544-144">VDD (patilla 27F)</span><span class="sxs-lookup"><span data-stu-id="89544-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="89544-145">3V (patilla 8A)</span><span class="sxs-lookup"><span data-stu-id="89544-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="89544-146">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="89544-146">Red cable</span></span>     |
| <span data-ttu-id="89544-147">DATOS (patilla 28F)</span><span class="sxs-lookup"><span data-stu-id="89544-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="89544-148">GPIO 2 (patilla 9A)</span><span class="sxs-lookup"><span data-stu-id="89544-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="89544-149">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="89544-149">White cable</span></span>    |
| <span data-ttu-id="89544-150">GND (patilla 30F)</span><span class="sxs-lookup"><span data-stu-id="89544-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="89544-151">GND (patilla 7J)</span><span class="sxs-lookup"><span data-stu-id="89544-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="89544-152">Cable negro</span><span class="sxs-lookup"><span data-stu-id="89544-152">Black cable</span></span>   |


- <span data-ttu-id="89544-153">Para obtener más información, consulte [el programa de instalación del sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) y [las especificaciones de Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).</span><span class="sxs-lookup"><span data-stu-id="89544-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="89544-154">Ahora su Sparkfun ESP8266 Thing Dev debe estar conectado con un sensor de trabajo.</span><span class="sxs-lookup"><span data-stu-id="89544-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![conectar dht22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="89544-156">Conectar el equipo de desarrollo de Sparkfun ESP8266 lo tooyour</span><span class="sxs-lookup"><span data-stu-id="89544-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="89544-157">Utilice Sparkfun ESP8266 lo Dev tooyour equipo de hello Micro USB tooType A USB cable tooconnect como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="89544-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![conectar compacto huzzah tooyour equipo](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="89544-159">Adición de permisos de puerto (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="89544-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="89544-160">Si usas Ubuntu, asegúrese de que un usuario normal tenga Hola permisos toooperate en hello USB puerto de Sparkfun ESP8266 lo dev.</span><span class="sxs-lookup"><span data-stu-id="89544-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="89544-161">permisos de puerto serie tooadd para un usuario normal, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="89544-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="89544-162">Ejecute hello siguientes comandos en un terminal:</span><span class="sxs-lookup"><span data-stu-id="89544-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="89544-163">Obtener una Hola siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="89544-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="89544-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="89544-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="89544-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="89544-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="89544-166">En la salida de hello, tenga en cuenta `uucp` o `dialout` decir Hola grupo nombre del propietario de hello puerto USB.</span><span class="sxs-lookup"><span data-stu-id="89544-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="89544-167">Agregar grupo de toohello de hello usuarios ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="89544-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="89544-168">`<group-owner-name>`es el nombre de propietario de grupo de Hola que obtuvo en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="89544-169">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="89544-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="89544-170">Cierre sesión Ubuntu y vuelva a iniciar en ella para cambiar tootake efecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="89544-171">Recopilar datos del sensor y enviarla tooyour centro de IoT</span><span class="sxs-lookup"><span data-stu-id="89544-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="89544-172">En esta sección, implementará y ejecutará una aplicación de ejemplo en Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="89544-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="89544-173">aplicación de ejemplo de Hola parpadea Hola LED en Sparkfun ESP8266 lo Dev y envía la temperatura de Hola y recopilan los datos de humedad de hello DHT22 sensor tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="89544-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="89544-174">Obtener la aplicación de ejemplo de Hola desde GitHub</span><span class="sxs-lookup"><span data-stu-id="89544-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="89544-175">aplicación de ejemplo de Hola se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="89544-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="89544-176">Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="89544-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="89544-177">repositorio de ejemplo de Hola tooclone, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="89544-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="89544-178">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="89544-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="89544-179">Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.</span><span class="sxs-lookup"><span data-stu-id="89544-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="89544-180">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="89544-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="89544-181">Instalar el paquete de Hola para Sparkfun ESP8266 lo Dev en Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="89544-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="89544-182">Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="89544-183">Abra el archivo de app.ino de hello en la carpeta de la aplicación hello en Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="89544-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Abra la aplicación de ejemplo de Hola en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="89544-185">Hola Arduino IDE, haga clic en **archivo** > **preferencias**.</span><span class="sxs-lookup"><span data-stu-id="89544-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="89544-186">Hola **preferencias** diálogo cuadro, haga clic en hello icono siguiente toohello **más direcciones URL del Administrador de paneles** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="89544-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="89544-187">En la ventana emergente de hello, escriba Hola después de la dirección URL y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89544-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![dirección url del paquete de punto tooa arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="89544-189">Hola **preferencias** cuadro de diálogo, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89544-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="89544-190">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.</span><span class="sxs-lookup"><span data-stu-id="89544-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="89544-191">Se instalará ESP8266 con una versión de 2.2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="89544-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Hola esp8266 paquete está instalado](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="89544-193">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="89544-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="89544-194">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="89544-194">Install necessary libraries</span></span>

1. <span data-ttu-id="89544-195">Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.</span><span class="sxs-lookup"><span data-stu-id="89544-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="89544-196">Busque Hola siguiendo los nombres de las bibliotecas uno por uno.</span><span class="sxs-lookup"><span data-stu-id="89544-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="89544-197">Para cada biblioteca de Hola que encuentre, haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="89544-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="89544-198">¿No tiene un sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="89544-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="89544-199">aplicación de ejemplo de Hola puede simular la temperatura y humedad datos en caso de que no tiene un sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="89544-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="89544-200">datos de toouse simulado de la aplicación de ejemplo de tooenable hello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="89544-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="89544-201">Abra hello `config.h` archivo Hola `app` carpeta.</span><span class="sxs-lookup"><span data-stu-id="89544-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="89544-202">Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="89544-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="89544-204">Guarde con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="89544-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="89544-205">Implementar tooSparkfun de aplicación de ejemplo de Hola ESP8266 lo desarrollo</span><span class="sxs-lookup"><span data-stu-id="89544-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="89544-206">Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola para Sparkfun ESP8266 lo dev</span><span class="sxs-lookup"><span data-stu-id="89544-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="89544-207">Haga clic en **boceto** > **cargar** toobuild e implementar tooSparkfun de aplicación de ejemplo de Hola ESP8266 lo dev</span><span class="sxs-lookup"><span data-stu-id="89544-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="89544-208">Si usas macOS probablemente percibirá Hola siguientes mensajes durante la carga.</span><span class="sxs-lookup"><span data-stu-id="89544-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="89544-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="89544-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="89544-210">Abra la ventana de ternimal y finalizar por debajo de acciones toosolve este problema.</span><span class="sxs-lookup"><span data-stu-id="89544-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="89544-211">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="89544-211">Enter your credentials</span></span>

<span data-ttu-id="89544-212">Una vez finalizada correctamente la carga de hello, siga Hola pasos tooenter sus credenciales:</span><span class="sxs-lookup"><span data-stu-id="89544-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="89544-213">Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.</span><span class="sxs-lookup"><span data-stu-id="89544-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="89544-214">En la ventana del monitor de la serie de hello, observe listas desplegables de hello dos en hello esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="89544-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="89544-215">Seleccione **ningún final de línea** de lista desplegable de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="89544-216">Seleccione **115.200 baudios** para la lista desplegable derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="89544-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="89544-217">En cuadro de entrada de hello situado en parte superior de saludo de la ventana del monitor de la serie de hello, escriba Hola siguiente información si se le solicita tooprovide y, a continuación, haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="89544-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="89544-218">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="89544-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="89544-219">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="89544-219">Wi-Fi password</span></span>
   * <span data-ttu-id="89544-220">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="89544-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="89544-221">información de credenciales de Hola se almacena en hello EEPROM de Sparkfun ESP8266 lo dev.</span><span class="sxs-lookup"><span data-stu-id="89544-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="89544-222">Si hace clic en botón de restablecimiento de hello en hello Sparkfun ESP8266 lo Dev panel, aplicación de ejemplo de Hola se le preguntará si desea obtener información de hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="89544-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="89544-223">Escriba `Y` toohave Hola información borrado y se le pide información de hello tooprovide nuevo.</span><span class="sxs-lookup"><span data-stu-id="89544-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="89544-224">Compruebe la aplicación de ejemplo de Hola se esté ejecutando correctamente</span><span class="sxs-lookup"><span data-stu-id="89544-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="89544-225">Si ve siguiente Hola de salida de la ventana del monitor de la serie de Hola y Hola parpadear LED de Sparkfun ESP8266 lo Dev, aplicación de ejemplo de Hola se está ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="89544-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![salida final en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="89544-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89544-227">Next steps</span></span>

<span data-ttu-id="89544-228">Está correctamente conectado un centro de IoT tooyour Sparkfun ESP8266 lo Dev y envía el centro de IoT de hello capturan sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="89544-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
