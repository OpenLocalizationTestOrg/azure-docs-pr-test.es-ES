---
title: aaaESP8266 toocloud - conectar compacto HUZZAH ESP8266 tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conéctese de plataforma de nube de Azure de toosend datos toohello Adafruit compacto HUZZAH ESP8266 tooAzure centro de IoT para él en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="b881c-103">Conectar Adafruit compacto HUZZAH ESP8266 tooAzure centro de IoT en nube Hola</span><span class="sxs-lookup"><span data-stu-id="b881c-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre DHT22, Feather HUZZAH ESP8266 e IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="b881c-105">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="b881c-105">What you do</span></span>


<span data-ttu-id="b881c-106">Conectar el centro de IoT de tooan Adafruit compacto HUZZAH ESP8266 creados por usted.</span><span class="sxs-lookup"><span data-stu-id="b881c-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="b881c-107">A continuación, ejecutar una aplicación de ejemplo en ESP8266 toocollect Hola temperatura y humedad los datos de un sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="b881c-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="b881c-108">Por último, envíe centro de IoT de hello sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b881c-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="b881c-109">Si usa otros paneles ESP8266, aún puede seguir estos pasos tooconnect, centro de IoT tooyour.</span><span class="sxs-lookup"><span data-stu-id="b881c-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="b881c-110">Función que está usando el panel de hello ESP8266, podría necesitar tooreconfigure Hola `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="b881c-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="b881c-111">Por ejemplo, si usa ESP8266 de AI Pensador, puede cambiar de `0` demasiado`2`.</span><span class="sxs-lookup"><span data-stu-id="b881c-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="b881c-112">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="b881c-112">Don't have a kit yet?</span></span> <span data-ttu-id="b881c-113">Obtener de hello [sitio Web de Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="b881c-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="b881c-114">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="b881c-114">What you learn</span></span>

* <span data-ttu-id="b881c-115">¿Cómo toocreate un centro de IoT y registrar un dispositivo de desvanecimiento HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b881c-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b881c-116">¿Cómo tooconnect compacto HUZZAH ESP8266 con sensor de Hola y el equipo</span><span class="sxs-lookup"><span data-stu-id="b881c-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="b881c-117">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en compacto HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b881c-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="b881c-118">¿Cómo toosend Hola centro de IoT de sensor datos tooyour</span><span class="sxs-lookup"><span data-stu-id="b881c-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b881c-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="b881c-119">What you need</span></span>

![Piezas necesarias para el tutorial de Hola](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="b881c-121">toocomplete esta operación, necesita Hola siguientes partes de su compacto HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="b881c-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="b881c-122">Hola compacto HUZZAH ESP8266 panel</span><span class="sxs-lookup"><span data-stu-id="b881c-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="b881c-123">Un cable USB A tooType de Micro USB</span><span class="sxs-lookup"><span data-stu-id="b881c-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="b881c-124">También necesita Hola después cosas para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="b881c-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="b881c-125">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="b881c-125">An active Azure subscription.</span></span> <span data-ttu-id="b881c-126">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="b881c-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="b881c-127">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b881c-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="b881c-128">Red inalámbrica para compacto HUZZAH ESP8266 tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="b881c-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="b881c-129">Herramienta de configuración de Hola de toodownload de la conexión de Internet.</span><span class="sxs-lookup"><span data-stu-id="b881c-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="b881c-130">[IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="b881c-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="b881c-131">Las versiones anteriores no funcionan con la biblioteca de AzureIoT Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="b881c-132">Hello elementos siguientes son opcionales en caso de que no tiene un sensor.</span><span class="sxs-lookup"><span data-stu-id="b881c-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="b881c-133">También tiene Hola opción consiste en utilizar datos de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="b881c-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="b881c-134">Un sensor de temperatura y humedad Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="b881c-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="b881c-135">Una placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="b881c-135">A breadboard</span></span>
* <span data-ttu-id="b881c-136">Cables de puente M/M</span><span class="sxs-lookup"><span data-stu-id="b881c-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="b881c-137">Conectar compacto HUZZAH ESP8266 con sensor de Hola y el equipo</span><span class="sxs-lookup"><span data-stu-id="b881c-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="b881c-138">En esta sección, se conecta tooyour placa de hello sensores.</span><span class="sxs-lookup"><span data-stu-id="b881c-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="b881c-139">A continuación, conectar el equipo de tooyour de dispositivo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="b881c-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="b881c-140">Conectar un tooFeather de sensor DHT22 temperatura y humedad HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b881c-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="b881c-141">Utilice hello breadboard y puentes cables toomake Hola conexión como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="b881c-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="b881c-142">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="b881c-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referencia de conexiones](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="b881c-144">Para el PIN de sensor, use Hola después de conectar:</span><span class="sxs-lookup"><span data-stu-id="b881c-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="b881c-145">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="b881c-145">Start (Sensor)</span></span>           | <span data-ttu-id="b881c-146">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="b881c-146">End (Board)</span></span>           | <span data-ttu-id="b881c-147">Color de cable</span><span class="sxs-lookup"><span data-stu-id="b881c-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="b881c-148">VDD (patilla 31F)</span><span class="sxs-lookup"><span data-stu-id="b881c-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="b881c-149">3V (patilla 58H)</span><span class="sxs-lookup"><span data-stu-id="b881c-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="b881c-150">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="b881c-150">Red cable</span></span>     |
| <span data-ttu-id="b881c-151">DATOS (patilla 32F)</span><span class="sxs-lookup"><span data-stu-id="b881c-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="b881c-152">GPIO 2 (patilla 46)</span><span class="sxs-lookup"><span data-stu-id="b881c-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="b881c-153">Cable azul</span><span class="sxs-lookup"><span data-stu-id="b881c-153">Blue cable</span></span>    |
| <span data-ttu-id="b881c-154">GND (patilla 34F)</span><span class="sxs-lookup"><span data-stu-id="b881c-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="b881c-155">GND (patilla 56I)</span><span class="sxs-lookup"><span data-stu-id="b881c-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="b881c-156">Cable negro</span><span class="sxs-lookup"><span data-stu-id="b881c-156">Black cable</span></span>   |

<span data-ttu-id="b881c-157">Para más información, consulte la [instalación del sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) y el [patillaje de Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="b881c-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="b881c-158">Ahora su Feather Huzzah ESP8266 debe estar conectado con un sensor de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b881c-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Conectar DHT22 con Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="b881c-160">Conectar compacto HUZZAH ESP8266 tooyour equipo</span><span class="sxs-lookup"><span data-stu-id="b881c-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="b881c-161">Tal y como se muestra a continuación, usar compacto HUZZAH ESP8266 tooyour equipo de hello Micro USB tooType A USB cable tooconnect.</span><span class="sxs-lookup"><span data-stu-id="b881c-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Conectar compacto Huzzah tooyour equipo](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="b881c-163">Agregar permisos de puerto serie (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b881c-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="b881c-164">Si usas Ubuntu, asegúrese de que tiene Hola permisos toooperate en hello USB puerto de desvanecimiento HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b881c-165">permisos de puerto serie tooadd, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b881c-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="b881c-166">Ejecute hello siguientes comandos en un terminal:</span><span class="sxs-lookup"><span data-stu-id="b881c-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="b881c-167">Obtener una Hola siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="b881c-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="b881c-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b881c-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="b881c-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="b881c-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="b881c-170">En la salida de hello, tenga en cuenta que `uucp` o `dialout` es nombre de propietario del grupo de Hola de hello puerto USB.</span><span class="sxs-lookup"><span data-stu-id="b881c-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="b881c-171">Agregar grupo de toohello de hello usuarios ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b881c-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="b881c-172">`<group-owner-name>`es el nombre de propietario de grupo de Hola que obtuvo en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="b881c-173">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b881c-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="b881c-174">Cierre la sesión de Ubuntu y, a continuación, inicie la sesión para tooappear de cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="b881c-175">Recopilar datos del sensor y enviarla tooyour centro de IoT</span><span class="sxs-lookup"><span data-stu-id="b881c-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="b881c-176">En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b881c-177">aplicación de ejemplo de Hola parpadea Hola LED de desvanecimiento HUZZAH ESP8266 y envía la temperatura de Hola y recopilan los datos de humedad de hello DHT22 sensor tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="b881c-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="b881c-178">Obtener la aplicación de ejemplo de Hola desde GitHub</span><span class="sxs-lookup"><span data-stu-id="b881c-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="b881c-179">aplicación de ejemplo de Hola se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="b881c-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="b881c-180">Clonar el repositorio de ejemplo de Hola que contiene la aplicación de ejemplo de Hola desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="b881c-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="b881c-181">repositorio de ejemplo de Hola tooclone, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b881c-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="b881c-182">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="b881c-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="b881c-183">Vaya carpeta tooa donde desea toobe de aplicación de ejemplo de Hola almacenado.</span><span class="sxs-lookup"><span data-stu-id="b881c-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="b881c-184">Ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b881c-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="b881c-185">Instalar el paquete de Hola para compacto HUZZAH ESP8266 Hola Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="b881c-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="b881c-186">Abra la carpeta de Hola donde se almacena la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="b881c-187">Abra el archivo de app.ino de hello en la carpeta de la aplicación Hola Hola Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="b881c-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Abra la aplicación de ejemplo de Hola en Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="b881c-189">Hola Arduino IDE, haga clic en **archivo** > **preferencias**.</span><span class="sxs-lookup"><span data-stu-id="b881c-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="b881c-190">Hola **preferencias** diálogo cuadro, haga clic en hello icono siguiente toohello **más direcciones URL del Administrador de paneles** cuadro.</span><span class="sxs-lookup"><span data-stu-id="b881c-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="b881c-191">En la ventana emergente de hello, escriba Hola después de la dirección URL y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b881c-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Dirección url del paquete de punto tooa Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="b881c-193">Hola **preferencias** cuadro de diálogo, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="b881c-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="b881c-194">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="b881c-195">El administrador de placas indica que está instalado ESP8266 con la versión 2.2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="b881c-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Hola esp8266 paquete está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="b881c-197">Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="b881c-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="b881c-198">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="b881c-198">Install necessary libraries</span></span>

1. <span data-ttu-id="b881c-199">Hola Arduino IDE, haga clic en **boceto** > **incluyen biblioteca** > **administrar bibliotecas de**.</span><span class="sxs-lookup"><span data-stu-id="b881c-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="b881c-200">Busque Hola siguiendo los nombres de las bibliotecas uno por uno.</span><span class="sxs-lookup"><span data-stu-id="b881c-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="b881c-201">Para cada biblioteca que encuentre, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="b881c-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="b881c-202">¿No tiene un sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="b881c-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="b881c-203">aplicación de ejemplo de Hola puede simular la temperatura y humedad datos en caso de que no tiene un sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="b881c-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="b881c-204">tooset los datos de toouse simulado de aplicación de ejemplo Hola, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="b881c-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="b881c-205">Abra hello `config.h` archivo Hola `app` carpeta.</span><span class="sxs-lookup"><span data-stu-id="b881c-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="b881c-206">Busque Hola después de la línea de código y cambie el valor de Hola de `false` demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="b881c-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar datos de toouse simulado de aplicación de ejemplo de Hola](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="b881c-208">Guardar archivo de hello con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="b881c-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="b881c-209">Implementar tooFeather de aplicación de ejemplo de Hola HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="b881c-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="b881c-210">Hola Arduino IDE, haga clic en **herramienta** > **puerto**y, a continuación, haga clic en puerto serie Hola de desvanecimiento HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="b881c-211">Haga clic en **boceto** > **cargar** toobuild e implementar tooFeather de aplicación de ejemplo de Hola HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="b881c-212">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="b881c-212">Enter your credentials</span></span>

<span data-ttu-id="b881c-213">Una vez finalizada correctamente la carga de hello, siga estos pasos tooenter sus credenciales:</span><span class="sxs-lookup"><span data-stu-id="b881c-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="b881c-214">Hola Arduino IDE, haga clic en **herramientas** > **Monitor serie**.</span><span class="sxs-lookup"><span data-stu-id="b881c-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="b881c-215">En la ventana del monitor de la serie de hello, tenga en cuenta listas desplegables de hello dos en la esquina inferior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="b881c-216">Seleccione **ningún final de línea** de lista desplegable de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="b881c-217">Seleccione **115.200 baudios** para la lista desplegable derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="b881c-218">En cuadro de entrada de hello situado en parte superior de saludo de la ventana del monitor de la serie de hello, escriba Hola siguiente información si se le solicita tooprovide y, a continuación, haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="b881c-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="b881c-219">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b881c-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="b881c-220">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="b881c-220">Wi-Fi password</span></span>
   * <span data-ttu-id="b881c-221">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="b881c-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="b881c-222">información de credenciales de Hola se almacena en hello EEPROM de desvanecimiento HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="b881c-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="b881c-223">Si hace clic en botón de restablecimiento de hello en Hola panel compacto HUZZAH ESP8266, aplicación de ejemplo de Hola le preguntará si desea que tooerase información de Hola.</span><span class="sxs-lookup"><span data-stu-id="b881c-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="b881c-224">Escriba `Y` información de hello toohave borrado.</span><span class="sxs-lookup"><span data-stu-id="b881c-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="b881c-225">Se le pide información de hello tooprovide una segunda vez.</span><span class="sxs-lookup"><span data-stu-id="b881c-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="b881c-226">Compruebe la aplicación de ejemplo de Hola se esté ejecutando correctamente</span><span class="sxs-lookup"><span data-stu-id="b881c-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="b881c-227">Si ve siguiente Hola de salida de la ventana del monitor de la serie de Hola y Hola parpadear LED de desvanecimiento HUZZAH ESP8266, aplicación de ejemplo de Hola se está ejecutando correctamente.</span><span class="sxs-lookup"><span data-stu-id="b881c-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Salida final en el IDE de Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="b881c-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b881c-229">Next steps</span></span>

<span data-ttu-id="b881c-230">Está correctamente conectado un centro de IoT de desvanecimiento HUZZAH ESP8266 tooyour y envía el centro de IoT de hello capturan sensor datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="b881c-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

