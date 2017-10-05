---
title: "Conexión de Raspberry Pi (C) a Azure IoT: Lección 1: Implementación de la aplicación | Microsoft Docs"
description: "Clone la aplicación de C de ejemplo de GitHub y use Gulp para implementar esta aplicación en la placa de Raspberry Pi 3. Esta aplicación de ejemplo hace parpadear el LED conectado a la placa cada dos segundos."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: intermitencia de led de raspberry pi, led intermitente con raspberry pi
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: f601d1e1-2bc3-4cc5-a6b1-0467e5304dcf
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 2ae409c6a39521711777ec329d2507a2801cc985
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="4fbf7-105">Creación e implementación de la aplicación de intermitencia</span><span class="sxs-lookup"><span data-stu-id="4fbf7-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4fbf7-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="4fbf7-106">What you will do</span></span>
<span data-ttu-id="4fbf7-107">Clone la aplicación de C de ejemplo de GitHub y use la herramienta Gulp para implementar la aplicación de ejemplo en Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-107">Clone the sample C application from GitHub, and use the gulp tool to deploy the sample application to Raspberry Pi 3.</span></span> <span data-ttu-id="4fbf7-108">La aplicación de ejemplo hace parpadear el LED conectado a la placa cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-108">The sample application blinks the LED connected to the board every two seconds.</span></span> <span data-ttu-id="4fbf7-109">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4fbf7-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4fbf7-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="4fbf7-110">What you will learn</span></span>
<span data-ttu-id="4fbf7-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-111">In this article, you will learn:</span></span>

* <span data-ttu-id="4fbf7-112">Cómo utilizar la herramienta `device-discover-cli` para recuperar la información de red de Pi</span><span class="sxs-lookup"><span data-stu-id="4fbf7-112">How to use the `device-discover-cli` tool to retrieve networking information about Pi.</span></span>
* <span data-ttu-id="4fbf7-113">Cómo implementar y ejecutar la aplicación de ejemplo en Pi</span><span class="sxs-lookup"><span data-stu-id="4fbf7-113">How to deploy and run the sample application on Pi.</span></span>
* <span data-ttu-id="4fbf7-114">Cómo implementar y depurar aplicaciones que se ejecutan de forma remota en Pi</span><span class="sxs-lookup"><span data-stu-id="4fbf7-114">How to deploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4fbf7-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="4fbf7-115">What you need</span></span>
<span data-ttu-id="4fbf7-116">Debe haber completado correctamente las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-116">You must have successfully completed the following operations:</span></span>

* [<span data-ttu-id="4fbf7-117">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="4fbf7-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="4fbf7-118">Obtener las herramientas</span><span class="sxs-lookup"><span data-stu-id="4fbf7-118">Get the tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-the-ip-address-and-host-name-of-pi"></a><span data-ttu-id="4fbf7-119">Obtención de la dirección IP y el nombre de host de Pi</span><span class="sxs-lookup"><span data-stu-id="4fbf7-119">Obtain the IP address and host name of Pi</span></span>
<span data-ttu-id="4fbf7-120">Abra un símbolo del sistema en Windows o una ventana de terminal de Mac OS o Ubuntu y, después, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run the following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="4fbf7-121">Debería ver una salida similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-121">You should see an output that is similar to the following:</span></span>

![Detección de dispositivos](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="4fbf7-123">Tome nota de los valores de `IP address` y `hostname` de Pi.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-123">Take note of the `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="4fbf7-124">Necesitará esta información posteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4fbf7-125">Asegúrese de que la Pi se conecta a la misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-125">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="4fbf7-126">Por ejemplo, si el equipo está conectado a una red inalámbrica mientras Pi está conectada a una red cableada, es posible que no vea la dirección IP en la salida de devdisco.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-126">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="4fbf7-127">Apertura de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4fbf7-127">Open the sample application</span></span>
<span data-ttu-id="4fbf7-128">Para abrir la aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-128">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="4fbf7-129">Clone el repositorio de ejemplo de GitHub ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-129">Clone the sample repository from GitHub by running the following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="4fbf7-130">Abra la aplicación de ejemplo en Visual Studio Code ejecutando los comandos siguientes:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-130">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="4fbf7-132">El archivo `main.c` de la subcarpeta `app` es el archivo de origen de la clave que contiene el código para controlar el LED.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-132">The `main.c` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="4fbf7-133">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4fbf7-133">Install application dependencies</span></span>
<span data-ttu-id="4fbf7-134">Instale las bibliotecas y otros módulos que necesite para la aplicación de ejemplo ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-134">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="4fbf7-135">Configuración de la conexión de dispositivos</span><span class="sxs-lookup"><span data-stu-id="4fbf7-135">Configure the device connection</span></span>
<span data-ttu-id="4fbf7-136">Para configurar la conexión de dispositivos, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-136">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="4fbf7-137">Genere el archivo de configuración de dispositivos mediante la ejecución del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-137">Generate the device configuration file by running the following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="4fbf7-138">El archivo de configuración `config-raspberrypi.json` contiene las credenciales de usuario que use para iniciar sesión en Pi.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-138">The configuration file `config-raspberrypi.json` contains the user credentials you use to log in to Pi.</span></span> <span data-ttu-id="4fbf7-139">Para evitar la pérdida de las credenciales de usuario, se genera el archivo de configuración en la subcarpeta `.iot-hub-getting-started` de la carpeta principal del equipo.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-139">To avoid the leak of user credentials, the configuration file is generated in the subfolder `.iot-hub-getting-started` of the home folder on your computer.</span></span>

2. <span data-ttu-id="4fbf7-140">Abra el archivo de configuración de dispositivos en Visual Studio Code ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-140">Open the device configuration file in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="4fbf7-141">Reemplace el marcador de posición `[device hostname or IP address]` con la dirección IP o el nombre de host que obtuvo anteriormente en "Obtención de la dirección IP y el nombre de host de Pi".</span><span class="sxs-lookup"><span data-stu-id="4fbf7-141">Replace the placeholder `[device hostname or IP address]` with the IP address or the host name that you got previously in "Obtain the IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="4fbf7-143">Puede usar la clave SSH en lugar del nombre de usuario y la contraseña al conectarse a Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-143">You can use SSH key instead of user name and password when connecting to Raspberry Pi.</span></span> <span data-ttu-id="4fbf7-144">Para ello se deben generar la clave mediante **ssh-keygen** y **ssh-copy-Id. pi @\<dirección del dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-144">In order to do this you will have to generate the key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="4fbf7-145">En Windows, estos comandos están disponibles en **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="4fbf7-146">En Mac OS, debe ejecutar **brew install ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-146">On MacOS you need to run **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="4fbf7-147">Después de cargar correctamente la clave en Raspberry Pi, reemplace **device_password** por la propiedad **device_key_path** en **config-raspberrypi.json**.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-147">After successfully uploading the key to the Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="4fbf7-148">Las líneas actualizadas deben presentar el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="4fbf7-149">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="4fbf7-149">Congratulations!</span></span> <span data-ttu-id="4fbf7-150">Ha creado correctamente la primera aplicación de ejemplo para Pi.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-150">You've successfully created the first sample application for Pi.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4fbf7-151">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4fbf7-151">Deploy and run the sample application</span></span>
### <a name="install-the-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="4fbf7-152">Instalación del SDK de IoT de Azure en Pi</span><span class="sxs-lookup"><span data-stu-id="4fbf7-152">Install the Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="4fbf7-153">Instale el SDK de IoT de Azure en Pi ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-153">Install the Azure IoT Hub SDK on Pi by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="4fbf7-154">Esta tarea podría tardar unos minutos en completarse la primera vez que la ejecute.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-154">This task might take a few minutes to complete the first time you run it.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="4fbf7-155">Implementación y ejecución de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4fbf7-155">Deploy and run the sample app</span></span>
<span data-ttu-id="4fbf7-156">Implemente y ejecute la aplicación de ejemplo usando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fbf7-156">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-the-app-works"></a><span data-ttu-id="4fbf7-157">Comprobación del funcionamiento de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4fbf7-157">Verify the app works</span></span>
<span data-ttu-id="4fbf7-158">La aplicación de ejemplo se finaliza automáticamente después de que el LED parpadee 20 veces.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-158">The sample application terminates automatically after the LED blinks for 20 times.</span></span> <span data-ttu-id="4fbf7-159">En caso contrario, consulte la [guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para ver soluciones a problemas comunes.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-159">If you don’t see the LED blinking, see the [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions to common problems.</span></span>
<span data-ttu-id="4fbf7-160">![Intermitencia del LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="4fbf7-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="4fbf7-161">Resumen</span><span class="sxs-lookup"><span data-stu-id="4fbf7-161">Summary</span></span>
<span data-ttu-id="4fbf7-162">Ha instalado las herramientas necesarias para usar Pi e implementado una aplicación de ejemplo para que Pi haga parpadear el LED.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-162">You've installed the required tools to work with Pi and deployed a sample application to Pi to blink the LED.</span></span> <span data-ttu-id="4fbf7-163">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que conecte Pi a Azure IoT Hub para enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="4fbf7-163">You can now create, deploy, and run another sample application that connects Pi to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fbf7-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fbf7-164">Next steps</span></span>
[<span data-ttu-id="4fbf7-165">Obtención de las herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="4fbf7-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

