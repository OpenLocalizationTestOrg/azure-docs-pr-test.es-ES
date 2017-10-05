---
title: "ESP8266 en la nube: conexión de Feather HUZZAH ESP8266 a Azure IoT Hub | Microsoft Docs"
description: "Con este tutorial aprenderá a configurar y conectar Adafruit Feather HUZZAH ESP8266 a Azure IoT Hub para que envíe datos a la plataforma en la nube de Azure."
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="5ae56-103">Conexión de Adafruit Feather HUZZAH ESP8266 a Azure IoT Hub en la nube</span><span class="sxs-lookup"><span data-stu-id="5ae56-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexión entre DHT22, Feather HUZZAH ESP8266 e IoT Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="5ae56-105">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="5ae56-105">What you do</span></span>


<span data-ttu-id="5ae56-106">Cree una conexión entre Adafruit Feather HUZZAH ESP8266 e IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="5ae56-107">Luego, ejecutará una aplicación de ejemplo en ESP8266 para recopilar datos de temperatura y humedad desde un sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="5ae56-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="5ae56-108">Por último, envíe los datos del sensor a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="5ae56-109">Aunque use otras placas ESP8266, puede seguir estos pasos para conectarse a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="5ae56-110">Dependiendo de la placa ESP8266 que use, puede que deba volver a configurar el `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="5ae56-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="5ae56-111">Por ejemplo, si usa ESP8266 de AI-Thinker, puede cambiarlo de `0` a `2`.</span><span class="sxs-lookup"><span data-stu-id="5ae56-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="5ae56-112">¿Aún no tiene un kit?</span><span class="sxs-lookup"><span data-stu-id="5ae56-112">Don't have a kit yet?</span></span> <span data-ttu-id="5ae56-113">Consígalo en el [sitio web de Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="5ae56-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="5ae56-114">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="5ae56-114">What you learn</span></span>

* <span data-ttu-id="5ae56-115">Cómo crear una instancia de IoT Hub y registrar un dispositivo para Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5ae56-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="5ae56-116">Cómo conectar Feather HUZZAH ESP8266 con el sensor y el equipo</span><span class="sxs-lookup"><span data-stu-id="5ae56-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="5ae56-117">Cómo recopilar datos del sensor mediante la ejecución de una aplicación de ejemplo en Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5ae56-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="5ae56-118">Cómo enviar los datos del sensor a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5ae56-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5ae56-119">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="5ae56-119">What you need</span></span>

![Elementos necesarios para el tutorial](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="5ae56-121">Para realizar esta operación, necesita los siguientes elementos del kit de inicio de Feather HUZZAH ESP8266:</span><span class="sxs-lookup"><span data-stu-id="5ae56-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="5ae56-122">La placa Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5ae56-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="5ae56-123">Un cable micro USB a USB tipo A</span><span class="sxs-lookup"><span data-stu-id="5ae56-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="5ae56-124">También necesitará lo siguiente para el entorno de desarrollo:</span><span class="sxs-lookup"><span data-stu-id="5ae56-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="5ae56-125">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="5ae56-125">An active Azure subscription.</span></span> <span data-ttu-id="5ae56-126">Si no tiene ninguna cuenta de Azure, [cree una cuenta de evaluación gratuita de Azure](https://azure.microsoft.com/free/) en solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="5ae56-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="5ae56-127">Un equipo PC o Mac que ejecute Windows o Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5ae56-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="5ae56-128">Red inalámbrica a la que se conectará HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="5ae56-129">Conexión a Internet para descargar la herramienta de configuración.</span><span class="sxs-lookup"><span data-stu-id="5ae56-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="5ae56-130">[IDE de Arduino](https://www.arduino.cc/en/main/software) versión 1.6.8 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5ae56-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="5ae56-131">Las versiones anteriores no funcionan con la biblioteca de AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="5ae56-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="5ae56-132">Los elementos siguientes son opcionales en caso de que no tenga un sensor.</span><span class="sxs-lookup"><span data-stu-id="5ae56-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="5ae56-133">También tiene la opción de usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="5ae56-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="5ae56-134">Un sensor de temperatura y humedad Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="5ae56-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="5ae56-135">Una placa de pruebas</span><span class="sxs-lookup"><span data-stu-id="5ae56-135">A breadboard</span></span>
* <span data-ttu-id="5ae56-136">Cables de puente M/M</span><span class="sxs-lookup"><span data-stu-id="5ae56-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="5ae56-137">Conexión de Feather HUZZAH ESP8266 con el sensor y el equipo</span><span class="sxs-lookup"><span data-stu-id="5ae56-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="5ae56-138">En esta sección se conectan los sensores a la placa.</span><span class="sxs-lookup"><span data-stu-id="5ae56-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="5ae56-139">Luego se conecta el dispositivo al equipo para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="5ae56-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="5ae56-140">Conexión de un sensor de humedad y temperatura DHT22 a Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5ae56-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="5ae56-141">Use la placa de pruebas y los cables de puente para realizar la conexión del modo siguiente.</span><span class="sxs-lookup"><span data-stu-id="5ae56-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="5ae56-142">Si no dispone de un sensor, omita esta sección porque en su lugar puede usar una simulación de datos del sensor.</span><span class="sxs-lookup"><span data-stu-id="5ae56-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referencia de conexiones](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="5ae56-144">En las patillas del sensor, use el siguiente cableado:</span><span class="sxs-lookup"><span data-stu-id="5ae56-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="5ae56-145">Inicio (sensor)</span><span class="sxs-lookup"><span data-stu-id="5ae56-145">Start (Sensor)</span></span>           | <span data-ttu-id="5ae56-146">Fin (placa)</span><span class="sxs-lookup"><span data-stu-id="5ae56-146">End (Board)</span></span>           | <span data-ttu-id="5ae56-147">Color de cable</span><span class="sxs-lookup"><span data-stu-id="5ae56-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="5ae56-148">VDD (patilla 31F)</span><span class="sxs-lookup"><span data-stu-id="5ae56-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="5ae56-149">3V (patilla 58H)</span><span class="sxs-lookup"><span data-stu-id="5ae56-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="5ae56-150">Cable rojo</span><span class="sxs-lookup"><span data-stu-id="5ae56-150">Red cable</span></span>     |
| <span data-ttu-id="5ae56-151">DATOS (patilla 32F)</span><span class="sxs-lookup"><span data-stu-id="5ae56-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="5ae56-152">GPIO 2 (patilla 46)</span><span class="sxs-lookup"><span data-stu-id="5ae56-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="5ae56-153">Cable azul</span><span class="sxs-lookup"><span data-stu-id="5ae56-153">Blue cable</span></span>    |
| <span data-ttu-id="5ae56-154">GND (patilla 34F)</span><span class="sxs-lookup"><span data-stu-id="5ae56-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="5ae56-155">GND (patilla 56I)</span><span class="sxs-lookup"><span data-stu-id="5ae56-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="5ae56-156">Cable negro</span><span class="sxs-lookup"><span data-stu-id="5ae56-156">Black cable</span></span>   |

<span data-ttu-id="5ae56-157">Para más información, consulte la [instalación del sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) y el [patillaje de Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="5ae56-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="5ae56-158">Ahora su Feather Huzzah ESP8266 debe estar conectado con un sensor de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5ae56-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Conectar DHT22 con Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="5ae56-160">Conexión de Feather HUZZAH ESP8266 a su equipo</span><span class="sxs-lookup"><span data-stu-id="5ae56-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="5ae56-161">Como se indica a continuación, use el cable micro USB a USB tipo A para conectar Feather HUZZAH ESP8266 a su equipo de la manera siguiente.</span><span class="sxs-lookup"><span data-stu-id="5ae56-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Conectar Feather Huzzah al equipo](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="5ae56-163">Agregar permisos de puerto serie (solo Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="5ae56-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="5ae56-164">Si usa Ubuntu, asegúrese de que tiene los permisos para trabajar en el puerto USB de Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="5ae56-165">Para agregar permisos de puerto serie, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5ae56-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="5ae56-166">Ejecute los siguientes comandos en un terminal:</span><span class="sxs-lookup"><span data-stu-id="5ae56-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="5ae56-167">Obtendrá una de las siguientes salidas:</span><span class="sxs-lookup"><span data-stu-id="5ae56-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="5ae56-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5ae56-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="5ae56-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="5ae56-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="5ae56-170">En la salida, observe que `uucp` o `dialout` es el nombre del propietario del grupo del puerto USB.</span><span class="sxs-lookup"><span data-stu-id="5ae56-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="5ae56-171">Agregue el usuario al grupo mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ae56-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="5ae56-172">`<group-owner-name>` es el nombre del propietario del grupo que obtuvo en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="5ae56-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="5ae56-173">`<username>` es el nombre de usuario de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="5ae56-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="5ae56-174">Cierre la sesión de Ubuntu y luego vuelva a iniciar sesión para que aparezca el cambio.</span><span class="sxs-lookup"><span data-stu-id="5ae56-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="5ae56-175">Recopilación de datos del sensor y envío al centro de IoT</span><span class="sxs-lookup"><span data-stu-id="5ae56-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="5ae56-176">En esta sección, implementará y ejecutará una aplicación de ejemplo en Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="5ae56-177">La aplicación de ejemplo hace parpadear el LED en Feather HUZZAH ESP8266 y envía los datos de humedad y temperatura recopilados del sensor DHT22 a la instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="5ae56-178">Obtención de la aplicación de ejemplo de Github</span><span class="sxs-lookup"><span data-stu-id="5ae56-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="5ae56-179">La aplicación de ejemplo se hospeda en GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="5ae56-180">Clone el repositorio de ejemplos que contiene la aplicación de ejemplo de GitHub.</span><span class="sxs-lookup"><span data-stu-id="5ae56-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="5ae56-181">Para clonar el repositorio de ejemplos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5ae56-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="5ae56-182">Abra un símbolo del sistema o una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="5ae56-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="5ae56-183">Vaya a la carpeta donde desea almacenar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5ae56-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="5ae56-184">Ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5ae56-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="5ae56-185">Instale el paquete de Feather HUZZAH ESP8266 en el IDE de Arduino:</span><span class="sxs-lookup"><span data-stu-id="5ae56-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="5ae56-186">Abra la carpeta donde se almacena la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5ae56-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="5ae56-187">Abra el archivo app.ino en la carpeta de la aplicación en el IDE de Arduino.</span><span class="sxs-lookup"><span data-stu-id="5ae56-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Abrir la aplicación de ejemplo en el IDE de Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="5ae56-189">En Arduino IDE, haga clic en **File** >  (Archivo) **Preferences** (Preferencias).</span><span class="sxs-lookup"><span data-stu-id="5ae56-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="5ae56-190">En el cuadro de diálogo **Preferences** (Preferencias), haga clic en el icono junto al cuadro de diálogo **Additional Boards Manager URLs** (URL adicionales del gestor de placas).</span><span class="sxs-lookup"><span data-stu-id="5ae56-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="5ae56-191">En la ventana emergente, escriba la dirección URL siguiente y, a continuación, haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="5ae56-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Apuntar a una url de paquete en el IDE de Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="5ae56-193">En el cuadro de diálogo **Preference** (Preferencias), haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="5ae56-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="5ae56-194">Haga clic en **Tools** (Herramientas)  > **Board** (Placa)  > **Boards Manager** (Administrador de placas) y busque esp8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="5ae56-195">El administrador de placas indica que está instalado ESP8266 con la versión 2.2.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="5ae56-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Se instala el paquete esp8266](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="5ae56-197">Haga clic en **Tools** >  (Herramientas) **Board** >  (Placa) **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="5ae56-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="5ae56-198">Instalación de las bibliotecas necesarias</span><span class="sxs-lookup"><span data-stu-id="5ae56-198">Install necessary libraries</span></span>

1. <span data-ttu-id="5ae56-199">En Arduino IDE, haga clic en **Sketch** >  (Boceto) **Include Library** >  (Incluir biblioteca) **Manage Libraries** (Administrar bibliotecas).</span><span class="sxs-lookup"><span data-stu-id="5ae56-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="5ae56-200">Busque los nombres de biblioteca siguientes uno a uno.</span><span class="sxs-lookup"><span data-stu-id="5ae56-200">Search for the following library names one by one.</span></span> <span data-ttu-id="5ae56-201">Para cada biblioteca que encuentre, haga clic en **Install** (Instalar).</span><span class="sxs-lookup"><span data-stu-id="5ae56-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="5ae56-202">¿No tiene un sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="5ae56-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="5ae56-203">La aplicación de ejemplo puede simular datos de humedad y temperatura en caso de que no disponga de un sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="5ae56-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="5ae56-204">Para configurar la aplicación de ejemplo de modo que use datos simulados, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5ae56-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="5ae56-205">Abra el archivo `config.h` de la carpeta `app`.</span><span class="sxs-lookup"><span data-stu-id="5ae56-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="5ae56-206">Busque la siguiente línea de código y cambie el valor de `false` a `true`:</span><span class="sxs-lookup"><span data-stu-id="5ae56-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar la aplicación de ejemplo para usar datos simulados](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="5ae56-208">Guarde el archivo como `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="5ae56-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="5ae56-209">Implementación de la aplicación de ejemplo en Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="5ae56-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="5ae56-210">En Arduino IDE, haga clic en **Tool** >  (Herramienta) **Port** (Puerto) y haga clic en el puerto serie de Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="5ae56-211">Haga clic en **Sketch** >  (Boceto) **Upload** (Cargar) para compilar e implementar la aplicación de ejemplo en Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="5ae56-212">Escriba sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="5ae56-212">Enter your credentials</span></span>

<span data-ttu-id="5ae56-213">Cuando la carga finalice correctamente, siga estos pasos para escribir las credenciales:</span><span class="sxs-lookup"><span data-stu-id="5ae56-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="5ae56-214">En Arduino IDE, haga clic en **Tools** >  (Herramientas) **Serial Monitor** (Monitor serie).</span><span class="sxs-lookup"><span data-stu-id="5ae56-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="5ae56-215">En la ventana del monitor serie, observe las dos listas desplegables de la esquina inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="5ae56-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="5ae56-216">Seleccione **No line ending** (Sin final de línea) para la lista desplegable de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="5ae56-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="5ae56-217">Seleccione **115200 baud** (115200 baudios) para la lista desplegable derecha.</span><span class="sxs-lookup"><span data-stu-id="5ae56-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="5ae56-218">En el cuadro de entrada ubicado en la parte superior de la ventana del monitor serie, escriba la siguiente información si se le solicita y luego haga clic en **Send** (Enviar).</span><span class="sxs-lookup"><span data-stu-id="5ae56-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="5ae56-219">SSID de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5ae56-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="5ae56-220">Contraseña de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="5ae56-220">Wi-Fi password</span></span>
   * <span data-ttu-id="5ae56-221">Cadena de conexión de dispositivo</span><span class="sxs-lookup"><span data-stu-id="5ae56-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="5ae56-222">La información de credenciales se almacena en la EEPROM de Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="5ae56-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="5ae56-223">Si hace clic en el botón de restablecimiento de la placa Feather HUZZAH ESP8266, la aplicación de ejemplo le pregunta si desea borrar la información.</span><span class="sxs-lookup"><span data-stu-id="5ae56-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="5ae56-224">Escriba `Y` para borrar la información.</span><span class="sxs-lookup"><span data-stu-id="5ae56-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="5ae56-225">Se le pide que proporcione la información una segunda vez.</span><span class="sxs-lookup"><span data-stu-id="5ae56-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="5ae56-226">Compruebe que la aplicación de ejemplo se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="5ae56-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="5ae56-227">Si ve la siguiente salida de la ventana del monitor serie y el LED parpadeando en Feather HUZZAH ESP8266, la aplicación de ejemplo se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="5ae56-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Salida final en el IDE de Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="5ae56-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ae56-229">Next steps</span></span>

<span data-ttu-id="5ae56-230">Ha conectado correctamente un dispositivo Feather HUZZAH ESP8266 a su instancia de IoT Hub y ha enviado los datos de sensor capturados a esa instancia.</span><span class="sxs-lookup"><span data-stu-id="5ae56-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

