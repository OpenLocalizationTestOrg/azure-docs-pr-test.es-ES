---
title: "ESP8266 en la nube: conexión de Sparkfun ESP8266 Thing Dev a Azure IoT Hub | Microsoft Docs"
description: "Con este tutorial aprenderá a configurar y conectar Sparkfun ESP8266 Thing Dev a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
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
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="7f182-103">Conexión de Sparkfun ESP8266 Thing Dev a Azure IoT Hub en la nube</span><span class="sxs-lookup"><span data-stu-id="7f182-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexión entre DHT22, Thing Dev, y IoT Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="7f182-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="7f182-105">What you will do</span></span>

<span data-ttu-id="7f182-106">Conectará Sparkfun ESP8266 Thing Dev a un centro de IoT que creará.</span><span class="sxs-lookup"><span data-stu-id="7f182-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="7f182-107">Luego, ejecutará una aplicación de ejemplo en ESP8266 para recopilar datos de temperatura y humedad desde un sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="7f182-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="7f182-108">Por último, enviará los datos del sensor al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="7f182-109">Aunque use otras placas ESP8266, puede seguir estos pasos para conectarse a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="7f182-110">Dependiendo de la placa ESP8266 que use, puede que deba volver a configurar el `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="7f182-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="7f182-111">Por ejemplo, si usa ESP8266 de AI-Thinker, puede cambiarlo de `0` a `2`.</span><span class="sxs-lookup"><span data-stu-id="7f182-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="7f182-112">¿Aún no tiene el kit?, haga clic [aquí](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="7f182-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="7f182-113">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="7f182-113">What you will learn</span></span>

* <span data-ttu-id="7f182-114">Cómo crear un centro de IoT y registrar un dispositivo para Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="7f182-115">Cómo conectar Thing Dev con el sensor y el equipo.</span><span class="sxs-lookup"><span data-stu-id="7f182-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="7f182-116">Cómo recopilar datos del sensor mediante la ejecución de una aplicación de ejemplo en Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="7f182-117">Cómo enviar los datos del sensor al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="7f182-118">Qué necesita</span><span class="sxs-lookup"><span data-stu-id="7f182-118">What you will need</span></span>

![Elementos necesarios para el tutorial](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="7f182-120">Para completar esta operación, necesita las siguientes piezas del kit de inicio de Thing Dev:</span><span class="sxs-lookup"><span data-stu-id="7f182-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="7f182-121">La placa Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="7f182-122">Un cable micro USB a USB tipo A.</span><span class="sxs-lookup"><span data-stu-id="7f182-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="7f182-123">También necesitará lo siguiente para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="7f182-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="7f182-124">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="7f182-124">An active Azure subscription.</span></span> <span data-ttu-id="7f182-125">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7f182-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="7f182-126">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7f182-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="7f182-127">Red inalámbrica a la que se pueda conectar Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="7f182-128">Conexión a Internet para descargar la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="7f182-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="7f182-129">[Arduino IDE](https://www.arduino.cc/en/main/software) versión 1.6.8 (o posterior), ya que las versiones anteriores no funcionarán con la biblioteca de AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="7f182-130">Los elementos siguientes son opcionales en caso de que no tenga un sensor.</span><span class="sxs-lookup"><span data-stu-id="7f182-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="7f182-131">También tiene la opción de usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="7f182-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="7f182-132">Un sensor de temperatura y humedad Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="7f182-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="7f182-133">La placa de pruebas.</span><span class="sxs-lookup"><span data-stu-id="7f182-133">A breadboard.</span></span>
* <span data-ttu-id="7f182-134">Cables de puente M/M.</span><span class="sxs-lookup"><span data-stu-id="7f182-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="7f182-135">Conexión de ESP8266 Thing Dev con el sensor y el equipo</span><span class="sxs-lookup"><span data-stu-id="7f182-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="7f182-136">Conexión de un sensor de humedad y temperatura DHT22 a ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="7f182-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="7f182-137">Use la placa de pruebas y los cables de puente para realizar la conexión del modo siguiente.</span><span class="sxs-lookup"><span data-stu-id="7f182-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="7f182-138">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="7f182-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![referencia de conexiones](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="7f182-140">Para las patillas del sensor, usaremos el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="7f182-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="7f182-141">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="7f182-141">Start (Sensor)</span></span>           | <span data-ttu-id="7f182-142">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="7f182-142">End (Board)</span></span>           | <span data-ttu-id="7f182-143">Color de cable</span><span class="sxs-lookup"><span data-stu-id="7f182-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="7f182-144">VDD (patilla 27F)</span><span class="sxs-lookup"><span data-stu-id="7f182-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="7f182-145">3V (patilla 8A)</span><span class="sxs-lookup"><span data-stu-id="7f182-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="7f182-146">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="7f182-146">Red cable</span></span>     |
| <span data-ttu-id="7f182-147">DATOS (patilla 28F)</span><span class="sxs-lookup"><span data-stu-id="7f182-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="7f182-148">GPIO 2 (patilla 9A)</span><span class="sxs-lookup"><span data-stu-id="7f182-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="7f182-149">Cable blanco</span><span class="sxs-lookup"><span data-stu-id="7f182-149">White cable</span></span>    |
| <span data-ttu-id="7f182-150">GND (patilla 30F)</span><span class="sxs-lookup"><span data-stu-id="7f182-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="7f182-151">GND (patilla 7J)</span><span class="sxs-lookup"><span data-stu-id="7f182-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="7f182-152">Cable negro</span><span class="sxs-lookup"><span data-stu-id="7f182-152">Black cable</span></span>   |


- <span data-ttu-id="7f182-153">Para obtener más información, consulte [el programa de instalación del sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) y [las especificaciones de Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711).</span><span class="sxs-lookup"><span data-stu-id="7f182-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="7f182-154">Ahora su Sparkfun ESP8266 Thing Dev debe estar conectado con un sensor de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7f182-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![conectar dht22 con ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="7f182-156">Conexión de Sparkfun ESP8266 Thing Dev a su equipo</span><span class="sxs-lookup"><span data-stu-id="7f182-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="7f182-157">Use el cable micro USB a USB tipo A para conectar Sparkfun ESP8266 Thing Dev a su equipo de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="7f182-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![conectar feather huzzah a su equipo](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="7f182-159">Adición de permisos de puerto (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="7f182-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="7f182-160">Si usa Ubuntu, asegúrese de que un usuario normal tenga los permisos para trabajar en el puerto USB de Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7f182-161">Para agregar permisos de puerto serie para un usuario normal, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7f182-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="7f182-162">Ejecute los siguientes comandos en un terminal:</span><span class="sxs-lookup"><span data-stu-id="7f182-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="7f182-163">Obtendrá una de las siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="7f182-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="7f182-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="7f182-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="7f182-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="7f182-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="7f182-166">En la salida, observe `uucp` o `dialout`, que es el nombre del propietario del grupo del puerto USB.</span><span class="sxs-lookup"><span data-stu-id="7f182-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="7f182-167">Agregue el usuario al grupo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="7f182-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="7f182-168">`<group-owner-name>` es el nombre del propietario del grupo que obtuvo en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="7f182-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="7f182-169">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7f182-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="7f182-170">Cierre la sesión en Ubuntu e iníciela de nuevo para que el cambio surta efecto.</span><span class="sxs-lookup"><span data-stu-id="7f182-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="7f182-171">Recopilación de datos del sensor y envío al centro de IoT</span><span class="sxs-lookup"><span data-stu-id="7f182-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="7f182-172">En esta sección, implementará y ejecutará una aplicación de ejemplo en Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7f182-173">La aplicación de ejemplo hace parpadear el LED en Sparkfun ESP8266 Thing Dev y envía los datos de humedad y temperatura recopilados del sensor DHT22 al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="7f182-174">Obtención de la aplicación de ejemplo de Github</span><span class="sxs-lookup"><span data-stu-id="7f182-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="7f182-175">La aplicación de ejemplo se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f182-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="7f182-176">Clone el repositorio de ejemplos que contiene la aplicación de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="7f182-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="7f182-177">Para clonar el repositorio de ejemplos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7f182-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="7f182-178">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="7f182-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="7f182-179">Vaya a la carpeta donde desea almacenar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7f182-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="7f182-180">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="7f182-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="7f182-181">Instale el paquete para Sparkfun ESP8266 Thing Dev en Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="7f182-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="7f182-182">Abra la carpeta donde se almacena la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7f182-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="7f182-183">Abra el archivo app.ino en la carpeta de la aplicación en Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="7f182-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![abrir la aplicación de ejemplo en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="7f182-185">En Arduino IDE, haga clic en **File** >  (Archivo) **Preferences** (Preferencias).</span><span class="sxs-lookup"><span data-stu-id="7f182-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="7f182-186">En el cuadro de diálogo **Preferences** (Preferencias), haga clic en el icono junto al cuadro de texto **Additional Boards Manager URLs** (URL adicionales del gestor de placas).</span><span class="sxs-lookup"><span data-stu-id="7f182-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="7f182-187">En la ventana emergente, escriba la dirección URL siguiente y, a continuación, haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="7f182-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![apuntar a una url de paquete en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="7f182-189">En el cuadro de diálogo **Preference** (Preferencias), haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="7f182-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="7f182-190">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.</span><span class="sxs-lookup"><span data-stu-id="7f182-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="7f182-191">Se instalará ESP8266 con una versión de 2.2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7f182-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![se instala el paquete esp8266](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="7f182-193">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="7f182-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="7f182-194">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="7f182-194">Install necessary libraries</span></span>

1. <span data-ttu-id="7f182-195">En Arduino IDE, haga clic en **Sketch** >  (Boceto) **Include Library** >  (Incluir biblioteca) **Manage Libraries** (Administrar bibliotecas).</span><span class="sxs-lookup"><span data-stu-id="7f182-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="7f182-196">Busque los nombres de biblioteca siguientes uno a uno.</span><span class="sxs-lookup"><span data-stu-id="7f182-196">Search for the following library names one by one.</span></span> <span data-ttu-id="7f182-197">Para cada una de las bibliotecas que encuentre, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="7f182-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="7f182-198">¿No tiene un sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="7f182-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="7f182-199">La aplicación de ejemplo puede simular datos de humedad y temperatura en caso de que no disponga de un sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="7f182-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="7f182-200">Para permitir que la aplicación de ejemplo use datos simulados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7f182-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="7f182-201">Abra el archivo `config.h` de la carpeta `app`.</span><span class="sxs-lookup"><span data-stu-id="7f182-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="7f182-202">Busque la siguiente línea de código y cambie el valor de `false` a `true`:</span><span class="sxs-lookup"><span data-stu-id="7f182-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![configurar la aplicación de ejemplo para usar datos simulados](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="7f182-204">Guarde con `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="7f182-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="7f182-205">Implementación de la aplicación de ejemplo en Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="7f182-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="7f182-206">En Arduino IDE, haga clic en **Tool** >  (Herramienta) **Port** (Puerto) y haga clic en el puerto serie de Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="7f182-207">Haga clic en **Sketch** >  (Boceto) **Upload** (Cargar) para compilar e implementar la aplicación de ejemplo en Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="7f182-208">Si usa macOS, quizá vea los siguientes mensajes durante la carga.</span><span class="sxs-lookup"><span data-stu-id="7f182-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="7f182-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="7f182-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="7f182-210">Abra la ventana de terminal y realice las siguientes acciones para resolver este problema.</span><span class="sxs-lookup"><span data-stu-id="7f182-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="7f182-211">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="7f182-211">Enter your credentials</span></span>

<span data-ttu-id="7f182-212">Cuando la carga finalice correctamente, siga los pasos para escribir sus credenciales:</span><span class="sxs-lookup"><span data-stu-id="7f182-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="7f182-213">En Arduino IDE, haga clic en **Tools** >  (Herramientas) **Serial Monitor** (Monitor serie).</span><span class="sxs-lookup"><span data-stu-id="7f182-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="7f182-214">En la ventana de monitor serie, observe las dos listas desplegables de la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="7f182-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="7f182-215">Seleccione **No line ending** (Sin final de línea) para la lista desplegable de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="7f182-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="7f182-216">Seleccione **115200 baud** (115200 baudios) para la lista desplegable derecha.</span><span class="sxs-lookup"><span data-stu-id="7f182-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="7f182-217">En el cuadro de entrada ubicado en la parte superior de la ventana del monitor serie, escriba la siguiente información si se le solicita y luego haga clic en **Send** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="7f182-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="7f182-218">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="7f182-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="7f182-219">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="7f182-219">Wi-Fi password</span></span>
   * <span data-ttu-id="7f182-220">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="7f182-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="7f182-221">La información de credenciales se almacena en la EEPROM de Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="7f182-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="7f182-222">Si hace clic en el botón de restablecimiento de la placa Sparkfun ESP8266 Thing Dev, la aplicación de ejemplo le pregunta si desea borrar la información.</span><span class="sxs-lookup"><span data-stu-id="7f182-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="7f182-223">Escriba `Y` para que se borre la información y se le pida de nuevo.</span><span class="sxs-lookup"><span data-stu-id="7f182-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="7f182-224">Compruebe que la aplicación de ejemplo se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="7f182-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="7f182-225">Si ve la siguiente salida de la ventana del monitor serie y el LED parpadeando en Sparkfun ESP8266 Thing Dev, la aplicación de ejemplo se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="7f182-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![salida final en arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="7f182-227">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7f182-227">Next steps</span></span>

<span data-ttu-id="7f182-228">Ha conectado correctamente un dispositivo Sparkfun ESP8266 Thing Dev a su centro de IoT y ha enviado los datos de sensor capturados a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="7f182-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
