---
title: "Connect Raspberry PI (C) tooAzure IoT - lección 1: implementar la aplicación | Documentos de Microsoft"
description: "Clonar aplicación de ejemplo C hello desde GitHub y gulp toodeploy este panel de tooyour frambuesa Pi 3 de la aplicación. Esta aplicación de ejemplo parpadea Hola LED conectado toohello panel cada dos segundos."
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
ms.openlocfilehash: e90c3360c4de1873313db19561c781eb21dbf1d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="98f15-105">Crear e implementar la aplicación de hello parpadeo</span><span class="sxs-lookup"><span data-stu-id="98f15-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="98f15-106">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="98f15-106">What you will do</span></span>
<span data-ttu-id="98f15-107">Clonar aplicación de C de ejemplo de Hola desde GitHub y usar hello gulp herramienta toodeploy Hola ejemplo aplicación tooRaspberry 3 de Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-107">Clone hello sample C application from GitHub, and use hello gulp tool toodeploy hello sample application tooRaspberry Pi 3.</span></span> <span data-ttu-id="98f15-108">aplicación de ejemplo de Hola parpadea Hola LED conectado toohello panel cada dos segundos.</span><span class="sxs-lookup"><span data-stu-id="98f15-108">hello sample application blinks hello LED connected toohello board every two seconds.</span></span> <span data-ttu-id="98f15-109">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="98f15-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="98f15-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="98f15-110">What you will learn</span></span>
<span data-ttu-id="98f15-111">En este artículo, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="98f15-111">In this article, you will learn:</span></span>

* <span data-ttu-id="98f15-112">¿Cómo toouse hello `device-discover-cli` tooretrieve de herramienta de la red sobre Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-112">How toouse hello `device-discover-cli` tool tooretrieve networking information about Pi.</span></span>
* <span data-ttu-id="98f15-113">La ejecución hello y toodeploy aplicación sobre Pi de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="98f15-113">How toodeploy and run hello sample application on Pi.</span></span>
* <span data-ttu-id="98f15-114">¿Cómo toodeploy y depurar las aplicaciones ejecutando de forma remota en Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-114">How toodeploy and debug applications running remotely on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98f15-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="98f15-115">What you need</span></span>
<span data-ttu-id="98f15-116">Debe haber completado correctamente hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="98f15-116">You must have successfully completed hello following operations:</span></span>

* [<span data-ttu-id="98f15-117">Configuración del dispositivo</span><span class="sxs-lookup"><span data-stu-id="98f15-117">Configure your device</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md)
* [<span data-ttu-id="98f15-118">Obtener herramientas de Hola</span><span class="sxs-lookup"><span data-stu-id="98f15-118">Get hello tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson1-get-the-tools-win32.md)

## <a name="obtain-hello-ip-address-and-host-name-of-pi"></a><span data-ttu-id="98f15-119">Obtener nombre de host y dirección IP de Hola de Pi</span><span class="sxs-lookup"><span data-stu-id="98f15-119">Obtain hello IP address and host name of Pi</span></span>
<span data-ttu-id="98f15-120">Abra un símbolo del sistema en Windows o un terminal de Mac OS o Ubuntu y, a continuación, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="98f15-120">Open a command prompt in Windows or a terminal in macOS or Ubuntu, and then run hello following command:</span></span>

```bash
devdisco list --eth
```

<span data-ttu-id="98f15-121">Debería ver un resultado similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="98f15-121">You should see an output that is similar toohello following:</span></span>

![Detección de dispositivos](media/iot-hub-raspberry-pi-lessons/lesson1/device_discovery.png)

<span data-ttu-id="98f15-123">Tome nota de hello `IP address` y `hostname` de Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-123">Take note of hello `IP address` and `hostname` of Pi.</span></span> <span data-ttu-id="98f15-124">Necesitará esta información posteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="98f15-124">You need this information later in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="98f15-125">Asegúrese de que ese Pi está conectado toohello misma red que el equipo.</span><span class="sxs-lookup"><span data-stu-id="98f15-125">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="98f15-126">Por ejemplo, si el equipo está conectado tooa red inalámbrica mientras Pi es tooa conectado por cable de red, no verá Hola IP dirección en la salida de hello devdisco.</span><span class="sxs-lookup"><span data-stu-id="98f15-126">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="98f15-127">Aplicación de ejemplo de Hola abierto</span><span class="sxs-lookup"><span data-stu-id="98f15-127">Open hello sample application</span></span>
<span data-ttu-id="98f15-128">Hola tooopen aplicación de ejemplo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98f15-128">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="98f15-129">Clonar el repositorio de ejemplo de Hola desde GitHub ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98f15-129">Clone hello sample repository from GitHub by running hello following command:</span></span>
   
    ```bash
    git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started.git
    ```
2. <span data-ttu-id="98f15-130">Abra la aplicación de ejemplo de Hola en código de Visual Studio mediante la ejecución de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="98f15-130">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>
   
    ```bash
    cd iot-hub-c-raspberrypi-getting-started
    cd Lesson1
    code .
    ```

![Estructura del repositorio](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-blink-c-mac.png)

<span data-ttu-id="98f15-132">Hola `main.c` archivo Hola `app` subcarpeta es el archivo de origen de la clave de Hola que contiene Hola código toocontrol Hola LED.</span><span class="sxs-lookup"><span data-stu-id="98f15-132">hello `main.c` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="98f15-133">Instalación de las dependencias de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="98f15-133">Install application dependencies</span></span>
<span data-ttu-id="98f15-134">Instalar bibliotecas de Hola y otros módulos que necesita para la aplicación de ejemplo de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="98f15-134">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="98f15-135">Configurar conexión de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="98f15-135">Configure hello device connection</span></span>
<span data-ttu-id="98f15-136">tooconfigure Hola conexión del dispositivo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="98f15-136">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="98f15-137">Generar archivo de configuración de dispositivo de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98f15-137">Generate hello device configuration file by running hello following command:</span></span>
   
   ```bash
   gulp init
   ```
   
   <span data-ttu-id="98f15-138">archivo de configuración de Hello `config-raspberrypi.json` contiene las credenciales de usuario de hello usar toolog en tooPi.</span><span class="sxs-lookup"><span data-stu-id="98f15-138">hello configuration file `config-raspberrypi.json` contains hello user credentials you use toolog in tooPi.</span></span> <span data-ttu-id="98f15-139">pérdida de hello tooavoid de credenciales de usuario, se genera el archivo de configuración de hello en subcarpeta hello `.iot-hub-getting-started` de la carpeta particular de hello en el equipo.</span><span class="sxs-lookup"><span data-stu-id="98f15-139">tooavoid hello leak of user credentials, hello configuration file is generated in hello subfolder `.iot-hub-getting-started` of hello home folder on your computer.</span></span>

2. <span data-ttu-id="98f15-140">Abra el archivo de configuración de dispositivo de hello en código de Visual Studio mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98f15-140">Open hello device configuration file in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```

3. <span data-ttu-id="98f15-141">Reemplace el marcador de posición de hello `[device hostname or IP address]` con dirección IP de Hola o nombre de host de hello obtenido anteriormente en "Obtener Hola IP dirección y nombre de host de Pi."</span><span class="sxs-lookup"><span data-stu-id="98f15-141">Replace hello placeholder `[device hostname or IP address]` with hello IP address or hello host name that you got previously in "Obtain hello IP address and host name of Pi."</span></span>
   
   ![Config.json](media/iot-hub-raspberry-pi-lessons/lesson1/vscode-config-mac.png)

> [!NOTE]
> <span data-ttu-id="98f15-143">Puede usar la clave SSH en lugar del nombre de usuario y contraseña al conectar tooRaspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-143">You can use SSH key instead of user name and password when connecting tooRaspberry Pi.</span></span> <span data-ttu-id="98f15-144">En Ordenar toodo esto tendrá toogenerate Hola clave utilizando **ssh-keygen** y **ssh-copy-Id. pi @\<dirección del dispositivo\>**.</span><span class="sxs-lookup"><span data-stu-id="98f15-144">In order toodo this you will have toogenerate hello key using **ssh-keygen** and **ssh-copy-id pi@\<device address\>**.</span></span>
>
> <span data-ttu-id="98f15-145">En Windows, estos comandos están disponibles en **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="98f15-145">On Windows these commands are available in **Git Bash**.</span></span>
>
> <span data-ttu-id="98f15-146">En Mac OS necesita toorun **cerveza instalar ssh-copy-id**.</span><span class="sxs-lookup"><span data-stu-id="98f15-146">On MacOS you need toorun **brew install ssh-copy-id**.</span></span>
>
> <span data-ttu-id="98f15-147">Después de cargar correctamente Hola clave toohello frambuesa Pi, reemplace **device_password** con **device_key_path** propiedad en **raspberrypi.json config**.</span><span class="sxs-lookup"><span data-stu-id="98f15-147">After successfully uploading hello key toohello Raspberry Pi, replace **device_password** with **device_key_path** property in **config-raspberrypi.json**.</span></span>
>
> <span data-ttu-id="98f15-148">Las líneas actualizadas deben presentar el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="98f15-148">Updated lines should look as below:</span></span>
> ```javascript
> "device_user_name": "pi",
> "device_key_path": "id_rsa",
> ```

<span data-ttu-id="98f15-149">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="98f15-149">Congratulations!</span></span> <span data-ttu-id="98f15-150">Ha creado correctamente la primera aplicación de ejemplo hello de Pi.</span><span class="sxs-lookup"><span data-stu-id="98f15-150">You've successfully created hello first sample application for Pi.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="98f15-151">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="98f15-151">Deploy and run hello sample application</span></span>
### <a name="install-hello-azure-iot-hub-sdk-on-pi"></a><span data-ttu-id="98f15-152">Instalar hello Azure IoT Hub SDK en Pi</span><span class="sxs-lookup"><span data-stu-id="98f15-152">Install hello Azure IoT Hub SDK on Pi</span></span>
<span data-ttu-id="98f15-153">Instale hello Azure IoT Hub SDK sobre Pi con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98f15-153">Install hello Azure IoT Hub SDK on Pi by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="98f15-154">Esta tarea puede tardar unos Hola de toocomplete minutos primera vez que lo ejecute.</span><span class="sxs-lookup"><span data-stu-id="98f15-154">This task might take a few minutes toocomplete hello first time you run it.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="98f15-155">Implementar y ejecutar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="98f15-155">Deploy and run hello sample app</span></span>
<span data-ttu-id="98f15-156">Implementar y ejecutar la aplicación de ejemplo de Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="98f15-156">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="98f15-157">Compruebe que funciona de la aplicación de Hola</span><span class="sxs-lookup"><span data-stu-id="98f15-157">Verify hello app works</span></span>
<span data-ttu-id="98f15-158">aplicación de ejemplo de Hola finaliza automáticamente después de hello LED parpadea para 20 veces.</span><span class="sxs-lookup"><span data-stu-id="98f15-158">hello sample application terminates automatically after hello LED blinks for 20 times.</span></span> <span data-ttu-id="98f15-159">Si no ve Hola LED parpadea, vea hello [Guía de solución de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md) para soluciones toocommon problemas.</span><span class="sxs-lookup"><span data-stu-id="98f15-159">If you don’t see hello LED blinking, see hello [troubleshooting guide](iot-hub-raspberry-pi-kit-c-troubleshooting.md) for solutions toocommon problems.</span></span>
<span data-ttu-id="98f15-160">![Intermitencia del LED](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span><span class="sxs-lookup"><span data-stu-id="98f15-160">![LED blinking](media/iot-hub-raspberry-pi-lessons/lesson1/led_blinking.jpg)</span></span>

## <a name="summary"></a><span data-ttu-id="98f15-161">Resumen</span><span class="sxs-lookup"><span data-stu-id="98f15-161">Summary</span></span>
<span data-ttu-id="98f15-162">Ha instalado Hola requerido herramientas toowork con Pi e implementado un Hola de tooblink tooPi de aplicación de ejemplo LED.</span><span class="sxs-lookup"><span data-stu-id="98f15-162">You've installed hello required tools toowork with Pi and deployed a sample application tooPi tooblink hello LED.</span></span> <span data-ttu-id="98f15-163">Ahora puede crear, implementar y ejecutar otra aplicación de ejemplo que se conecta Pi tooAzure toosend centro de IoT y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="98f15-163">You can now create, deploy, and run another sample application that connects Pi tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98f15-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98f15-164">Next steps</span></span>
[<span data-ttu-id="98f15-165">Obtención de las herramientas de Azure</span><span class="sxs-lookup"><span data-stu-id="98f15-165">Get Azure tools</span></span>](iot-hub-raspberry-pi-kit-c-lesson2-get-azure-tools-win32.md)

