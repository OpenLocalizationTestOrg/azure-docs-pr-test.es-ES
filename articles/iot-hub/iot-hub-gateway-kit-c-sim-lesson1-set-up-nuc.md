---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 1: Configuración de NUC | Microsoft Docs"
description: "Configure Intel NUC para que funcione como puerta de enlace de IoT entre un sensor e IoT Hub de Azure para recopilar información del sensor y enviarla a IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: yjianfeng
tags: 
keywords: puerta de enlace de iot, intel nuc, equipo nuc, DE3815TYKE
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: f41d6b2e-9b00-40df-90eb-17d824bea883
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b87974be9570f7d03fe84ae0a1d1fa7e346ff189
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="f4235-104">Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="f4235-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f4235-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="f4235-105">What you will do</span></span>

- <span data-ttu-id="f4235-106">Configure Intel NUC como puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="f4235-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="f4235-107">Instale el paquete de Azure IoT Edge en Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f4235-107">Install the Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="f4235-108">Ejecute una aplicación de ejemplo "hola_mundo" en Intel NUC para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-108">Run a "hello_world" sample application on Intel NUC to verify the gateway functionality.</span></span>
<span data-ttu-id="f4235-109">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f4235-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f4235-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="f4235-110">What you will learn</span></span>

<span data-ttu-id="f4235-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4235-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="f4235-112">Conexión de Intel NUC con periféricos.</span><span class="sxs-lookup"><span data-stu-id="f4235-112">How to connect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="f4235-113">Instalación y actualización de los paquetes necesarios en Intel NUC mediante Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="f4235-113">How to install and update the required packages on Intel NUC using the Smart Package Manager.</span></span>
- <span data-ttu-id="f4235-114">Ejecución de una aplicación de ejemplo "hola_mundo" para comprobar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-114">How to run the "hello_world" sample application to verify the gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f4235-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="f4235-115">What you need</span></span>

- <span data-ttu-id="f4235-116">Un kit Intel NUC DE3815TYKE con Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="f4235-116">An Intel NUC Kit DE3815TYKE with the Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="f4235-117">Un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f4235-117">An Ethernet cable.</span></span>
- <span data-ttu-id="f4235-118">Un teclado.</span><span class="sxs-lookup"><span data-stu-id="f4235-118">A keyboard.</span></span>
- <span data-ttu-id="f4235-119">Un cable HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="f4235-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="f4235-120">Un monitor con un puerto HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="f4235-120">A monitor with an HDMI or VGA port.</span></span>

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-the-peripherals"></a><span data-ttu-id="f4235-122">Conexión de Intel NUC con los periféricos</span><span class="sxs-lookup"><span data-stu-id="f4235-122">Connect Intel NUC with the peripherals</span></span>

<span data-ttu-id="f4235-123">La imagen siguiente es un ejemplo de Intel NUC conectado con varios periféricos:</span><span class="sxs-lookup"><span data-stu-id="f4235-123">The image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="f4235-124">Conectado a un teclado.</span><span class="sxs-lookup"><span data-stu-id="f4235-124">Connected to a keyboard.</span></span>
2. <span data-ttu-id="f4235-125">Conectado al monitor mediante un cable VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="f4235-125">Connected to the monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="f4235-126">Conectado a una red cableada mediante un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="f4235-126">Connected to a wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="f4235-127">Conectado a la fuente de alimentación con un cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="f4235-127">Connected to the power supply with a power cable.</span></span>

![Intel NUC conectado a periféricos](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-to-the-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="f4235-129">Conexión al sistema Intel NUC desde el equipo host a través de Secure Shell (SSH)</span><span class="sxs-lookup"><span data-stu-id="f4235-129">Connect to the Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="f4235-130">Aquí necesita un teclado y un monitor para obtener la dirección IP del dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="f4235-130">Here you need keyboard and monitor to get the IP address of your NUC device.</span></span> <span data-ttu-id="f4235-131">Si ya conoce la dirección IP, puede ir al paso 3 de esta sección.</span><span class="sxs-lookup"><span data-stu-id="f4235-131">If you already know the IP address, you can skip to step 3 in this section.</span></span>

1. <span data-ttu-id="f4235-132">Encienda Intel NUC presionando el botón de encendido e inicie sesión en el sistema.</span><span class="sxs-lookup"><span data-stu-id="f4235-132">Turn on Intel NUC by pressing the Power button and log in the system.</span></span>

   <span data-ttu-id="f4235-133">El nombre de usuario y la contraseña predeterminados son `root`.</span><span class="sxs-lookup"><span data-stu-id="f4235-133">The default user name and password are both `root`.</span></span>

2. <span data-ttu-id="f4235-134">Obtenga la dirección IP de NUC mediante la ejecución del comando `ifconfig`.</span><span class="sxs-lookup"><span data-stu-id="f4235-134">Get the IP address of NUC by running the `ifconfig` command.</span></span> <span data-ttu-id="f4235-135">Este paso se realiza en el dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="f4235-135">This step is done on the NUC device.</span></span>

   <span data-ttu-id="f4235-136">Este es un ejemplo del resultado del comando.</span><span class="sxs-lookup"><span data-stu-id="f4235-136">Here is an example of the command output.</span></span>

   ![Salida de ifconfig que muestra la dirección IP de NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="f4235-138">En este ejemplo, el valor que sigue a `inet addr:` es la dirección IP que necesita si tiene previsto conectarse remotamente desde un equipo host a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f4235-138">In this example, the value that follows `inet addr:` is the IP address that you need when you plan to connect remotely from a host computer to Intel NUC.</span></span>

3. <span data-ttu-id="f4235-139">Utilice uno de los siguientes clientes SSH desde el equipo host para conectarse a Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f4235-139">Use one of the following SSH clients from your host machine to connect to Intel NUC.</span></span>

   - <span data-ttu-id="f4235-140">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="f4235-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="f4235-141">El cliente de SSH integrado en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="f4235-141">The build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="f4235-142">Resulta más eficaz y productivo operar en Intel NUC desde un equipo host.</span><span class="sxs-lookup"><span data-stu-id="f4235-142">It is more efficient and productive to operate on Intel NUC from a host computer.</span></span> <span data-ttu-id="f4235-143">Necesita la dirección IP, el nombre de usuario y la contraseña para conectarse a NUC a través del cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="f4235-143">You need the the IP address, user name and password to connect the NUC via SSH client.</span></span> <span data-ttu-id="f4235-144">Este es el ejemplo de cliente de SSH que se usa en macOS.</span><span class="sxs-lookup"><span data-stu-id="f4235-144">Here is the example use SSH client on macOS.</span></span>
   <span data-ttu-id="f4235-145">![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="f4235-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-the-azure-iot-edge-package"></a><span data-ttu-id="f4235-146">Instalación del paquete de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="f4235-146">Install the Azure IoT Edge package</span></span>

<span data-ttu-id="f4235-147">El paquete de Azure IoT Edge contiene los archivos binarios compilados previamente del SDK y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="f4235-147">The Azure IoT Edge package contains the pre-compiled binaries of the SDK and its dependencies.</span></span> <span data-ttu-id="f4235-148">Estos archivos binarios forman Azure IoT Edge, el SDK de IoT de Azure y las herramientas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="f4235-148">These binaries are Azure IoT Edge, the Azure IoT SDK and the corresponding tools.</span></span> <span data-ttu-id="f4235-149">El paquete también contiene una aplicación de ejemplo "hello_world" que se utiliza para validar la funcionalidad de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-149">The package also contains a "hello_world" sample application that is used to validate the gateway functionality.</span></span> <span data-ttu-id="f4235-150">IoT Edge es la parte principal de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-150">IoT Edge is the core part of the gateway.</span></span> <span data-ttu-id="f4235-151">Para instalar el paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f4235-151">To install the package, follow these steps:</span></span>

1. <span data-ttu-id="f4235-152">Agregue el repositorio de la nube de IoT mediante la ejecución de los comandos siguientes en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="f4235-152">Add the IoT cloud repository by running the following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="f4235-153">El comando `rpm` importa la clave rpm.</span><span class="sxs-lookup"><span data-stu-id="f4235-153">The `rpm` command imports the rpm key.</span></span> <span data-ttu-id="f4235-154">El comando `smart channel` agrega el canal rpm a Smart Package Manager.</span><span class="sxs-lookup"><span data-stu-id="f4235-154">The `smart channel` command adds the rpm channel to the Smart Package Manager.</span></span> <span data-ttu-id="f4235-155">Antes de ejecutar el comando `smart update`, verá una salida similar a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="f4235-155">Before you run the `smart update` command, you see an output like below.</span></span>

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="f4235-157">Instale el paquete ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4235-157">Install the package by running the following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="f4235-158">`packagegroup-cloud-azure` es el nombre del paquete.</span><span class="sxs-lookup"><span data-stu-id="f4235-158">`packagegroup-cloud-azure` is the name of the package.</span></span> <span data-ttu-id="f4235-159">El comando `smart install` se usa para instalar el paquete.</span><span class="sxs-lookup"><span data-stu-id="f4235-159">The `smart install` command is used to install the package.</span></span>

   <span data-ttu-id="f4235-160">Después de instalar el paquete, Intel NUC debería funcionar como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-160">After the package is installed, Intel NUC is expected to work as a gateway.</span></span>

## <a name="run-the-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="f4235-161">Ejecución de la aplicación de ejemplo "hola_mundo" de Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="f4235-161">Run the Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="f4235-162">Vaya a `azureiotgatewaysdk/samples` y ejecute la aplicación de ejemplo "hola_mundo".</span><span class="sxs-lookup"><span data-stu-id="f4235-162">Go to `azureiotgatewaysdk/samples` and run the sample "hello_world" sample application.</span></span> <span data-ttu-id="f4235-163">Esta aplicación de ejemplo crea una puerta de enlace del archivo `hello_world.json` y utiliza los componentes fundamentales de la arquitectura de Azure IoT Edge para registrar un mensaje de "Hola mundo" en un archivo cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="f4235-163">This sample application creates a gateway from the `hello_world.json` file and uses the fundamental components of the Azure IoT Edge architecture to log a hello world message to a file every 5 seconds.</span></span>

<span data-ttu-id="f4235-164">Puede ejecutar la aplicación de ejemplo "hola_mundo" ejecutando el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4235-164">You can run the sample "hello_world" sample application by running the following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="f4235-165">La aplicación de ejemplo produce el siguiente resultado si la funcionalidad de puerta de enlace funciona correctamente:</span><span class="sxs-lookup"><span data-stu-id="f4235-165">The sample application produces the following output if the gateway functionality is working correctly:</span></span>

![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="f4235-167">Si tiene problemas, busque soluciones en la [página de solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f4235-167">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="f4235-168">Resumen</span><span class="sxs-lookup"><span data-stu-id="f4235-168">Summary</span></span>

<span data-ttu-id="f4235-169">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f4235-169">Congratulations!</span></span> <span data-ttu-id="f4235-170">Ha terminado de configurar Intel NUC como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="f4235-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="f4235-171">Ahora está listo para pasar a la lección siguiente donde configurará el equipo host, creará una instancia de IoT hub de Azure y registrará el dispositivo lógico de la instancia de IoT Hub de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4235-171">Now you're ready to move on to the next lesson to set up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4235-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4235-172">Next steps</span></span>
[<span data-ttu-id="f4235-173">Preparación del equipo host y de IoT Hub de Azure</span><span class="sxs-lookup"><span data-stu-id="f4235-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
