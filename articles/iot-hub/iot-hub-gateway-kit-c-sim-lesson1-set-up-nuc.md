---
title: "Dispositivo simulado y puerta de enlace de Azure IoT: Lección 1: Configuración de NUC | Microsoft Docs"
description: "Intel NUC toowork configurado como una puerta de enlace de IoT entre un sensor y la información del sensor toocollect centro de IoT de Azure y enviar tooIoT concentrador."
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
ms.openlocfilehash: c2146c7cd8ca54adbd0af279364ec8484be1b45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="ba59a-104">Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="ba59a-104">Set up Intel NUC as an IoT gateway</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ba59a-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="ba59a-105">What you will do</span></span>

- <span data-ttu-id="ba59a-106">Configure Intel NUC como puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="ba59a-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="ba59a-107">Instalar paquete de hello borde de IoT de Azure en NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="ba59a-107">Install hello Azure IoT Edge package on Intel NUC.</span></span>
- <span data-ttu-id="ba59a-108">Ejecutar una aplicación de ejemplo "hello_world" en la funcionalidad de puerta de enlace de Intel NUC tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-108">Run a "hello_world" sample application on Intel NUC tooverify hello gateway functionality.</span></span>
<span data-ttu-id="ba59a-109">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ba59a-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ba59a-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="ba59a-110">What you will learn</span></span>

<span data-ttu-id="ba59a-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ba59a-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="ba59a-112">¿Cómo tooconnect Intel NUC con dispositivos periféricos.</span><span class="sxs-lookup"><span data-stu-id="ba59a-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="ba59a-113">¿Cómo tooinstall y actualizar paquetes de hello necesario sobre el uso de Intel NUC Hola inteligente Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="ba59a-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="ba59a-114">Cómo hello toorun "hello_world" ejemplo de funcionalidad de puerta de enlace de aplicaciones tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ba59a-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="ba59a-115">What you need</span></span>

- <span data-ttu-id="ba59a-116">Un Intel NUC Kit DE3815TYKE con hello Suite de Software de puerta de enlace de IoT de Intel (viento demarcación Linux * 7.0.0.13) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="ba59a-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span>
- <span data-ttu-id="ba59a-117">Un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ba59a-117">An Ethernet cable.</span></span>
- <span data-ttu-id="ba59a-118">Un teclado.</span><span class="sxs-lookup"><span data-stu-id="ba59a-118">A keyboard.</span></span>
- <span data-ttu-id="ba59a-119">Un cable HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="ba59a-119">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="ba59a-120">Un monitor con un puerto HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="ba59a-120">A monitor with an HDMI or VGA port.</span></span>

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit_without_sensortag.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="ba59a-122">Conectar Intel NUC con dispositivos periféricos de Hola</span><span class="sxs-lookup"><span data-stu-id="ba59a-122">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="ba59a-123">imagen de Hello siguiente es un ejemplo de NUC de Intel que está conectado a periféricos distintos:</span><span class="sxs-lookup"><span data-stu-id="ba59a-123">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="ba59a-124">Teclado tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="ba59a-124">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="ba59a-125">Conectado toohello monitor mediante un cable VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="ba59a-125">Connected toohello monitor by a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="ba59a-126">Red cableada mediante tooa conectado mediante un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="ba59a-126">Connected tooa wired network by an Ethernet cable.</span></span>
4. <span data-ttu-id="ba59a-127">Fuente de alimentación de toohello conectado con un cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="ba59a-127">Connected toohello power supply with a power cable.</span></span>

![Intel NUC conectado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="ba59a-129">Toohello Intel NUC sistema conectado a la del equipo host a través de Shell seguro (SSH)</span><span class="sxs-lookup"><span data-stu-id="ba59a-129">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="ba59a-130">Aquí necesitará teclado y monitor tooget Hola dirección IP del dispositivo NUC.</span><span class="sxs-lookup"><span data-stu-id="ba59a-130">Here you need keyboard and monitor tooget hello IP address of your NUC device.</span></span> <span data-ttu-id="ba59a-131">Si ya sabe Hola IP dirección, puede omitir toostep 3 en esta sección.</span><span class="sxs-lookup"><span data-stu-id="ba59a-131">If you already know hello IP address, you can skip toostep 3 in this section.</span></span>

1. <span data-ttu-id="ba59a-132">Activar Intel NUC presionando el botón de encendido de Hola y de registro en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-132">Turn on Intel NUC by pressing hello Power button and log in hello system.</span></span>

   <span data-ttu-id="ba59a-133">nombre de usuario predeterminado de Hola y la contraseña son ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="ba59a-133">hello default user name and password are both `root`.</span></span>

2. <span data-ttu-id="ba59a-134">Obtener dirección IP de Hola de NUC ejecutando hello `ifconfig` comando.</span><span class="sxs-lookup"><span data-stu-id="ba59a-134">Get hello IP address of NUC by running hello `ifconfig` command.</span></span> <span data-ttu-id="ba59a-135">Este paso se realiza en el dispositivo NUC Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-135">This step is done on hello NUC device.</span></span>

   <span data-ttu-id="ba59a-136">Este es un ejemplo de salida del comando Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-136">Here is an example of hello command output.</span></span>

   ![Salida de ifconfig que muestra la dirección IP de NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="ba59a-138">En este ejemplo, Hola valor siguiente `inet addr:` es dirección IP de Hola que necesita, si tiene previsto tooconnect remotamente desde un tooIntel del equipo host NUC.</span><span class="sxs-lookup"><span data-stu-id="ba59a-138">In this example, hello value that follows `inet addr:` is hello IP address that you need when you plan tooconnect remotely from a host computer tooIntel NUC.</span></span>

3. <span data-ttu-id="ba59a-139">Utilice uno de hello siguiendo a los clientes SSH de su tooIntel tooconnect de máquina de host NUC.</span><span class="sxs-lookup"><span data-stu-id="ba59a-139">Use one of hello following SSH clients from your host machine tooconnect tooIntel NUC.</span></span>

   - <span data-ttu-id="ba59a-140">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="ba59a-140">[PuTTY](http://www.putty.org/) for Windows.</span></span>
   - <span data-ttu-id="ba59a-141">Hola compilación en el cliente de SSH en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="ba59a-141">hello build-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="ba59a-142">Es más eficaz y productiva toooperate en Intel NUC desde un equipo host.</span><span class="sxs-lookup"><span data-stu-id="ba59a-142">It is more efficient and productive toooperate on Intel NUC from a host computer.</span></span> <span data-ttu-id="ba59a-143">Necesita la dirección IP de Hola Hola, nombre de usuario y contraseña tooconnect hello NUC mediante el cliente de SSH.</span><span class="sxs-lookup"><span data-stu-id="ba59a-143">You need hello hello IP address, user name and password tooconnect hello NUC via SSH client.</span></span> <span data-ttu-id="ba59a-144">Este es el cliente de SSH de uso de ejemplo de Hola en macOS.</span><span class="sxs-lookup"><span data-stu-id="ba59a-144">Here is hello example use SSH client on macOS.</span></span>
   <span data-ttu-id="ba59a-145">![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="ba59a-145">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="ba59a-146">Instalar el paquete de hello borde de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="ba59a-146">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="ba59a-147">paquete de Hello borde de IoT de Azure contiene archivos binarios precompilados de Hola de hello SDK y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="ba59a-147">hello Azure IoT Edge package contains hello pre-compiled binaries of hello SDK and its dependencies.</span></span> <span data-ttu-id="ba59a-148">Estos archivos binarios forman borde de IoT de Azure, Hola IoT de Azure SDK y herramientas correspondientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-148">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="ba59a-149">paquete de Hello también contiene una aplicación de ejemplo de "hello_world" es la funcionalidad de puerta de enlace de hello toovalidate usado.</span><span class="sxs-lookup"><span data-stu-id="ba59a-149">hello package also contains a "hello_world" sample application that is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="ba59a-150">Borde de IoT es parte del núcleo de Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="ba59a-150">IoT Edge is hello core part of hello gateway.</span></span> <span data-ttu-id="ba59a-151">Hola tooinstall del paquete, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ba59a-151">tooinstall hello package, follow these steps:</span></span>

1. <span data-ttu-id="ba59a-152">Agregar repositorio de nube de hello IoT ejecutando Hola siga los comandos en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="ba59a-152">Add hello IoT cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import http://iotdk.intel.com/misc/iot_pub.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   ```

   <span data-ttu-id="ba59a-153">Hola `rpm` comando importaciones Hola clave rpm.</span><span class="sxs-lookup"><span data-stu-id="ba59a-153">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="ba59a-154">Hola `smart channel` comando agrega rpm Hola canal toohello inteligente Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="ba59a-154">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="ba59a-155">Antes de ejecutar hello `smart update` comando, verá una salida similar a continuación.</span><span class="sxs-lookup"><span data-stu-id="ba59a-155">Before you run hello `smart update` command, you see an output like below.</span></span>

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

   ```bash
   smart update
   ```

2. <span data-ttu-id="ba59a-157">Instalar paquete Hola ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="ba59a-157">Install hello package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="ba59a-158">`packagegroup-cloud-azure`es el nombre de Hola de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="ba59a-158">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="ba59a-159">Hola `smart install` comando es paquete de hello tooinstall usado.</span><span class="sxs-lookup"><span data-stu-id="ba59a-159">hello `smart install` command is used tooinstall hello package.</span></span>

   <span data-ttu-id="ba59a-160">Después de instalar el paquete de hello, Intel NUC es toowork esperado como una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ba59a-160">After hello package is installed, Intel NUC is expected toowork as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="ba59a-161">Ejecutar aplicación de ejemplo de "hello_world" hello borde de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="ba59a-161">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="ba59a-162">Vaya demasiado`azureiotgatewaysdk/samples` y ejecute la aplicación de ejemplo de Hola ejemplo "hello_world".</span><span class="sxs-lookup"><span data-stu-id="ba59a-162">Go too`azureiotgatewaysdk/samples` and run hello sample "hello_world" sample application.</span></span> <span data-ttu-id="ba59a-163">Esta aplicación de ejemplo crea una puerta de enlace de hello `hello_world.json` archivo y usa los componentes fundamentales de Hola de hello borde de IoT de Azure arquitectura toolog un archivo de tooa de hello world mensaje cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="ba59a-163">This sample application creates a gateway from hello `hello_world.json` file and uses hello fundamental components of hello Azure IoT Edge architecture toolog a hello world message tooa file every 5 seconds.</span></span>

<span data-ttu-id="ba59a-164">Puede ejecutar la aplicación de ejemplo de "hello_world" de ejemplo de Hola ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="ba59a-164">You can run hello sample "hello_world" sample application by running hello following command:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="ba59a-165">aplicación de ejemplo de Hola produce siguiente de hello resultado si la funcionalidad de puerta de enlace de hello funciona correctamente:</span><span class="sxs-lookup"><span data-stu-id="ba59a-165">hello sample application produces hello following output if hello gateway functionality is working correctly:</span></span>

![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)

<span data-ttu-id="ba59a-167">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="ba59a-167">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="ba59a-168">Resumen</span><span class="sxs-lookup"><span data-stu-id="ba59a-168">Summary</span></span>

<span data-ttu-id="ba59a-169">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ba59a-169">Congratulations!</span></span> <span data-ttu-id="ba59a-170">Ha terminado de configurar Intel NUC como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="ba59a-170">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="ba59a-171">Ahora está listo toomove en toohello siguiente lección tooset el equipo host, crear un centro de IoT de Azure y registrar el dispositivo lógico de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="ba59a-171">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT hub and register your Azure IoT hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba59a-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ba59a-172">Next steps</span></span>
[<span data-ttu-id="ba59a-173">Preparación del equipo host y de IoT Hub de Azure</span><span class="sxs-lookup"><span data-stu-id="ba59a-173">Get your host computer and Azure IoT hub ready</span></span>](iot-hub-gateway-kit-c-sim-lesson2-get-the-tools-win32.md)
