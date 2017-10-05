---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 1: Configuración de Intel NUC | Microsoft Docs"
description: "Configure Intel NUC para que funcione como puerta de enlace de IoT entre un sensor e IoT Hub de Azure para recopilar información del sensor y enviarla a IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: puerta de enlace de iot, intel nuc, equipo nuc, DE3815TYKE
ms.assetid: 917090d6-35c2-495b-a620-ca6f9c02b317
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1a3a92ab8d08c6ed6f047208217c46022027157e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="64ea2-104">Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="64ea2-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="64ea2-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="64ea2-105">What you will do</span></span>

- <span data-ttu-id="64ea2-106">Configure Intel NUC como puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="64ea2-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="64ea2-107">Instale el paquete de Azure IoT Edge en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="64ea2-107">Install the Azure IoT Edge package on the Intel NUC.</span></span>
- <span data-ttu-id="64ea2-108">Ejecute una aplicación de ejemplo "hola_mundo" en Intel NUC para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-108">Run a "hello_world" sample application on the Intel NUC to verify the gateway functionality.</span></span>

  > <span data-ttu-id="64ea2-109">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="64ea2-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="64ea2-110">What you will learn</span></span>

<span data-ttu-id="64ea2-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="64ea2-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="64ea2-112">Conexión de Intel NUC con periféricos.</span><span class="sxs-lookup"><span data-stu-id="64ea2-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="64ea2-113">Instalación y actualización de los paquetes necesarios en Intel NUC mediante Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="64ea2-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="64ea2-114">Ejecución de una aplicación de ejemplo "hola_mundo" para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64ea2-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="64ea2-115">What you need</span></span>

- <span data-ttu-id="64ea2-116">Un kit Intel NUC DE3815TYKE con Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="64ea2-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="64ea2-117">[Haga clic aquí para comprar el producto Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="64ea2-117">[Click here to purchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="64ea2-118">Un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="64ea2-118">An Ethernet cable.</span></span>
- <span data-ttu-id="64ea2-119">Un teclado.</span><span class="sxs-lookup"><span data-stu-id="64ea2-119">A keyboard.</span></span>
- <span data-ttu-id="64ea2-120">Un cable HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="64ea2-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="64ea2-121">Un monitor con un puerto HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="64ea2-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="64ea2-122">Opcional: [SensorTag de Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="64ea2-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="64ea2-124">Conexión de Intel NUC con los periféricos</span><span class="sxs-lookup"><span data-stu-id="64ea2-124">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="64ea2-125">La imagen siguiente es un ejemplo de Intel NUC conectado con varios periféricos:</span><span class="sxs-lookup"><span data-stu-id="64ea2-125">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="64ea2-126">Conectado a un teclado.</span><span class="sxs-lookup"><span data-stu-id="64ea2-126">Connected to a keyboard.</span></span>
2. <span data-ttu-id="64ea2-127">Conectado a un monitor mediante un cable VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="64ea2-127">Connected to a monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="64ea2-128">Conectado a una red cableada mediante un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="64ea2-128">Connected to a wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="64ea2-129">Conectado a una fuente de alimentación con un cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="64ea2-129">Connected to a power supply with a power cable.</span></span>

![Intel NUC conectado a periféricos](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="64ea2-131">Conexión al sistema Intel NUC desde el equipo host a través de Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="64ea2-131">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="64ea2-132">Necesitará un teclado y un monitor para obtener la dirección IP del dispositivo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="64ea2-132">You will need a keyboard and a monitor to get the IP address of your Intel NUC device.</span></span> <span data-ttu-id="64ea2-133">Si ya conoce la dirección IP, puede avanzar al paso 3 de esta sección.</span><span class="sxs-lookup"><span data-stu-id="64ea2-133">If you already know the IP address, you can skip ahead to step 3 in this section.</span></span>

1. <span data-ttu-id="64ea2-134">Encienda Intel NUC presionando el botón de encendido y, a continuación, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="64ea2-134">Turn on the Intel NUC by pressing the power button and then log in.</span></span>

   <span data-ttu-id="64ea2-135">El nombre de usuario y la contraseña predeterminados son `root`.</span><span class="sxs-lookup"><span data-stu-id="64ea2-135">The default user name and password are both `root`.</span></span>

       > Hit the enter key on your keyboard if you see either of the following errors when you boot: 'A TPM error (7) occurred attempting to read a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="64ea2-136">Obtenga la dirección IP de Intel NUC mediante la ejecución del comando `ifconfig` en el dispositivo Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="64ea2-136">Get the IP address of the Intel NUC by running the `ifconfig` command on the Intel NUC device.</span></span>

   <span data-ttu-id="64ea2-137">Este es un ejemplo del resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="64ea2-137">Here is an example of the command output.</span></span>

   ![Salida de ifconfig que muestra la dirección IP de Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="64ea2-139">En este ejemplo, el valor que sigue a `inet addr:` es la dirección IP que necesita para conectarse desde un equipo host a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="64ea2-139">In this example, the value that follows `inet addr:` is the IP address that you need when connect to the Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="64ea2-140">Utilice uno de los siguientes clientes SSH desde el equipo host para conectarse a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="64ea2-140">Use one of the following SSH clients from your host computer to connect to Intel NUC.</span></span>

    - <span data-ttu-id="64ea2-141">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="64ea2-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="64ea2-142">El cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="64ea2-142">The built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="64ea2-143">Resulta más eficaz y productivo operar en Intel NUC desde un equipo host.</span><span class="sxs-lookup"><span data-stu-id="64ea2-143">It is more efficient and productive to operate an Intel NUC from a host computer.</span></span> <span data-ttu-id="64ea2-144">Necesitará la dirección IP, el nombre de usuario y la contraseña de NUC para conectarse a través de un cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="64ea2-144">You'll need the Intel NUC's IP address, user name and password to connect to it via an SSH client.</span></span> <span data-ttu-id="64ea2-145">Este es un ejemplo que utiliza un cliente de SSH en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="64ea2-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="64ea2-146">![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="64ea2-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="64ea2-147">Instalación del paquete de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="64ea2-147">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="64ea2-148">El paquete de Azure IoT Edge contiene los archivos binarios compilados previamente de IoT Edge y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="64ea2-148">The Azure IoT Edge package contains the pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="64ea2-149">Estos archivos binarios forman Azure IoT Edge, el SDK de IoT de Azure y las herramientas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="64ea2-149">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="64ea2-150">El paquete también contiene una aplicación de ejemplo "hola_mundo" que se utiliza para validar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-150">The package also contains a "hello_world" sample application is used to validate the gateway functionality.</span></span> <span data-ttu-id="64ea2-151">IoT Edge es la parte principal de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-151">IoT Edge is the core part of the gateway.</span></span> 

<span data-ttu-id="64ea2-152">Para instalar el paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="64ea2-152">Follow these steps to install the package.</span></span>

1. <span data-ttu-id="64ea2-153">Agregue el repositorio de la nube de IoT mediante la ejecución de los comandos siguientes en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="64ea2-153">Add the IoT Cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="64ea2-154">Escriba "y" cuando se le pregunte si incluir este canal.</span><span class="sxs-lookup"><span data-stu-id="64ea2-154">Enter 'y', when it prompts you to 'Include this channel?'</span></span>
   
   <span data-ttu-id="64ea2-155">Si recibe un error `import read failed(-1)`, use los comandos siguientes para resolver el problema:</span><span class="sxs-lookup"><span data-stu-id="64ea2-155">If you receive an `import read failed(-1)` error, use the following commands to resolve the issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="64ea2-156">El comando `rpm` importa la clave rpm.</span><span class="sxs-lookup"><span data-stu-id="64ea2-156">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="64ea2-157">El comando `smart channel` agrega el canal rpm a Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="64ea2-157">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="64ea2-158">Antes de ejecutar el comando `smart update`, verá una salida similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="64ea2-158">Before you run the `smart update` command, you will see an output like below.</span></span>

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="64ea2-160">Ejecute el comando de actualización inteligente:</span><span class="sxs-lookup"><span data-stu-id="64ea2-160">Execute the smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="64ea2-161">Instale la puerta de enlace de IoT de Azure ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="64ea2-161">Install the Azure IoT Gateway package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="64ea2-162">`packagegroup-cloud-azure` es el nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="64ea2-162">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="64ea2-163">El comando `smart install` se usa para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="64ea2-163">The `smart install` command is used to install the package.</span></span>

    > <span data-ttu-id="64ea2-164">Ejecute el siguiente comando si ve este error: "la clave pública no está disponible".</span><span class="sxs-lookup"><span data-stu-id="64ea2-164">Run the following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="64ea2-165">Reinicie el dispositivo Intel NUC si ve el siguiente error: "no package provides util-linux-dev" (ningún paquete proporciona util-linux-dev).</span><span class="sxs-lookup"><span data-stu-id="64ea2-165">Reboot the Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="64ea2-166">Después de instalar el paquete, Intel NUC está listo para funcionar como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-166">After the package is installed, Intel NUC is ready to function as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="64ea2-167">Ejecución de la aplicación de ejemplo "hola_mundo" de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="64ea2-167">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="64ea2-168">La siguiente aplicación de ejemplo crea una puerta de enlace desde un archivo `hello_world.json` y utiliza los componentes fundamentales de la arquitectura de Azure IoT Edge para registrar un mensaje de "Hola mundo" en un archivo (log.txt) cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="64ea2-168">The following sample application creates a gateway from a `hello_world.json` file and uses the fundamental components of Azure IoT Edge architecture to log a hello world message to a file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="64ea2-169">Puede ejecutar el ejemplo de "Hola mundo" mediante la ejecución de los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="64ea2-169">You can run the Hello World sample by executing the following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="64ea2-170">Permita que la aplicación "Hola mundo" se ejecute durante unos minutos y, a continuación, presione la tecla ENTRAR para detenerla.</span><span class="sxs-lookup"><span data-stu-id="64ea2-170">Let the Hello World application run for a few minutes and then hit the Enter key to stop it.</span></span>
<span data-ttu-id="64ea2-171">![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="64ea2-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="64ea2-172">Puede omitir los errores sobre control de argumento no válido (NULL) que aparecen tras pulsar Entrar.</span><span class="sxs-lookup"><span data-stu-id="64ea2-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="64ea2-173">Para comprobar que la puerta de enlace se ejecutó correctamente, abra el archivo log.txt que se encuentra ahora en la ![vista del directorio de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png) de la carpeta hola_mundo.</span><span class="sxs-lookup"><span data-stu-id="64ea2-173">You can verify that the gateway ran successfully by opening the log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="64ea2-174">Abra log.txt mediante el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="64ea2-174">Open log.txt using the following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="64ea2-175">A continuación, verá el contenido de log.txt, que será una salida con formato JSON de los mensajes de registro que se escribieron cada 5 segundos por parte del módulo "Hola mundo" de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-175">You will then see the contents of log.txt, which will be a JSON formatted output of the logging messages that were written every 5 seconds by the gateway Hello World module.</span></span>
<span data-ttu-id="64ea2-176">![vista de directorio de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="64ea2-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="64ea2-177">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="64ea2-177">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="64ea2-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="64ea2-178">Summary</span></span>

<span data-ttu-id="64ea2-179">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="64ea2-179">Congratulations!</span></span> <span data-ttu-id="64ea2-180">Ha terminado de configurar Intel NUC como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="64ea2-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="64ea2-181">Ahora está listo para pasar a la lección siguiente, donde configurará el equipo host, creará una instancia de Azure IoT Hub y registrará el dispositivo lógico de la instancia de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="64ea2-181">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64ea2-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="64ea2-182">Next steps</span></span>
[<span data-ttu-id="64ea2-183">Uso de una puerta de enlace de IoT para conectar un dispositivo a Azure IoT Hub</span><span class="sxs-lookup"><span data-stu-id="64ea2-183">Use an IoT gateway to connect a device to Azure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

