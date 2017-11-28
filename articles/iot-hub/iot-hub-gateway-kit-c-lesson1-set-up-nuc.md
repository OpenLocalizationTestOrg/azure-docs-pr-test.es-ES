---
title: "Dispositivo SensorTag y puerta de enlace de Azure IoT: Lección 1: Configuración de Intel NUC | Microsoft Docs"
description: "Intel NUC toowork configurado como una puerta de enlace de IoT entre un sensor y la información del sensor toocollect centro de IoT de Azure y enviar tooIoT concentrador."
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
ms.openlocfilehash: 7c3ab3b014713c7facb86b8e8622d70e60a960e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-intel-nuc-as-an-iot-gateway"></a><span data-ttu-id="12db7-104">Configuración de Intel NUC como puerta de enlace de IoT</span><span class="sxs-lookup"><span data-stu-id="12db7-104">Set up Intel NUC as an IoT gateway</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

## <a name="what-you-will-do"></a><span data-ttu-id="12db7-105">Lo que hará</span><span class="sxs-lookup"><span data-stu-id="12db7-105">What you will do</span></span>

- <span data-ttu-id="12db7-106">Configure Intel NUC como puerta de enlace de IoT.</span><span class="sxs-lookup"><span data-stu-id="12db7-106">Set up Intel NUC as an IoT gateway.</span></span>
- <span data-ttu-id="12db7-107">Instalar paquete de hello borde de IoT de Azure en hello NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="12db7-107">Install hello Azure IoT Edge package on hello Intel NUC.</span></span>
- <span data-ttu-id="12db7-108">Ejecutar una aplicación de ejemplo "hello_world" en la funcionalidad de puerta de enlace de Intel NUC tooverify Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-108">Run a "hello_world" sample application on hello Intel NUC tooverify hello gateway functionality.</span></span>

  > <span data-ttu-id="12db7-109">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="12db7-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="12db7-110">Lo qué aprenderá</span><span class="sxs-lookup"><span data-stu-id="12db7-110">What you will learn</span></span>

<span data-ttu-id="12db7-111">En esta lección, aprenderá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="12db7-111">In this lesson, you will learn:</span></span>

- <span data-ttu-id="12db7-112">¿Cómo tooconnect Intel NUC con dispositivos periféricos.</span><span class="sxs-lookup"><span data-stu-id="12db7-112">How tooconnect Intel NUC with peripherals.</span></span>
- <span data-ttu-id="12db7-113">¿Cómo tooinstall y actualizar paquetes de hello necesario sobre el uso de Intel NUC Hola inteligente Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="12db7-113">How tooinstall and update hello required packages on Intel NUC using hello Smart Package Manager.</span></span>
- <span data-ttu-id="12db7-114">Cómo hello toorun "hello_world" ejemplo de funcionalidad de puerta de enlace de aplicaciones tooverify Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-114">How toorun hello "hello_world" sample application tooverify hello gateway functionality.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="12db7-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="12db7-115">What you need</span></span>

- <span data-ttu-id="12db7-116">Un Intel NUC Kit DE3815TYKE con hello Suite de Software de puerta de enlace de IoT de Intel (viento demarcación Linux * 7.0.0.13) preinstalado.</span><span class="sxs-lookup"><span data-stu-id="12db7-116">An Intel NUC Kit DE3815TYKE with hello Intel IoT Gateway Software Suite (Wind River Linux *7.0.0.13) preinstalled.</span></span> <span data-ttu-id="12db7-117">[Haga clic aquí toopurchase Kit comercial de puerta de enlace de arboleda IoT](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span><span class="sxs-lookup"><span data-stu-id="12db7-117">[Click here toopurchase Grove IoT Commercial Gateway Kit](https://www.seeedstudio.com/Grove-IoT-Commercial-Gateway-Kit-p-2724.html).</span></span>
- <span data-ttu-id="12db7-118">Un cable Ethernet.</span><span class="sxs-lookup"><span data-stu-id="12db7-118">An Ethernet cable.</span></span>
- <span data-ttu-id="12db7-119">Un teclado.</span><span class="sxs-lookup"><span data-stu-id="12db7-119">A keyboard.</span></span>
- <span data-ttu-id="12db7-120">Un cable HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="12db7-120">An HDMI or VGA cable.</span></span>
- <span data-ttu-id="12db7-121">Un monitor con un puerto HDMI o VGA.</span><span class="sxs-lookup"><span data-stu-id="12db7-121">A monitor with an HDMI or VGA port.</span></span>
- <span data-ttu-id="12db7-122">Opcional: [SensorTag de Texas Instruments (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span><span class="sxs-lookup"><span data-stu-id="12db7-122">Optional: [Texas Instruments Sensor Tag (CC2650STK)](http://www.ti.com/tool/cc2650stk)</span></span>

![Kit de puerta de enlace](media/iot-hub-gateway-kit-lessons/lesson1/kit.png)

## <a name="connect-intel-nuc-with-hello-peripherals"></a><span data-ttu-id="12db7-124">Conectar Intel NUC con dispositivos periféricos de Hola</span><span class="sxs-lookup"><span data-stu-id="12db7-124">Connect Intel NUC with hello peripherals</span></span>

<span data-ttu-id="12db7-125">imagen de Hello siguiente es un ejemplo de NUC de Intel que está conectado a periféricos distintos:</span><span class="sxs-lookup"><span data-stu-id="12db7-125">hello image below is an example of Intel NUC that is connected with various peripherals:</span></span>

1. <span data-ttu-id="12db7-126">Teclado tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="12db7-126">Connected tooa keyboard.</span></span>
2. <span data-ttu-id="12db7-127">Conectado tooa monitor con un cable VGA o HDMI.</span><span class="sxs-lookup"><span data-stu-id="12db7-127">Connected tooa monitor with a VGA cable or HDMI cable.</span></span>
3. <span data-ttu-id="12db7-128">Red con un cable Ethernet cableada mediante tooa conectado.</span><span class="sxs-lookup"><span data-stu-id="12db7-128">Connected tooa wired network with an Ethernet cable.</span></span>
4. <span data-ttu-id="12db7-129">Fuente de alimentación de tooa conectado con un cable de alimentación.</span><span class="sxs-lookup"><span data-stu-id="12db7-129">Connected tooa power supply with a power cable.</span></span>

![Intel NUC conectado tooperipherals](media/iot-hub-gateway-kit-lessons/lesson1/nuc.png)

## <a name="connect-toohello-intel-nuc-system-from-host-computer-via-secure-shell-ssh"></a><span data-ttu-id="12db7-131">Toohello Intel NUC sistema conectado a la del equipo host a través de Shell seguro (SSH)</span><span class="sxs-lookup"><span data-stu-id="12db7-131">Connect toohello Intel NUC system from host computer via Secure Shell (SSH)</span></span>

<span data-ttu-id="12db7-132">Necesitará un teclado y una dirección IP de monitor tooget Hola del dispositivo NUC de Intel.</span><span class="sxs-lookup"><span data-stu-id="12db7-132">You will need a keyboard and a monitor tooget hello IP address of your Intel NUC device.</span></span> <span data-ttu-id="12db7-133">Si ya sabe Hola IP dirección, puede omitir anticipada toostep 3 en esta sección.</span><span class="sxs-lookup"><span data-stu-id="12db7-133">If you already know hello IP address, you can skip ahead toostep 3 in this section.</span></span>

1. <span data-ttu-id="12db7-134">Activar Hola Intel NUC presionando el botón de encendido de hello y, a continuación, inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="12db7-134">Turn on hello Intel NUC by pressing hello power button and then log in.</span></span>

   <span data-ttu-id="12db7-135">nombre de usuario predeterminado de Hola y la contraseña son ambos `root`.</span><span class="sxs-lookup"><span data-stu-id="12db7-135">hello default user name and password are both `root`.</span></span>

       > Hit hello enter key on your keyboard if you see either of hello following errors when you boot: 'A TPM error (7) occurred attempting tooread a pcr value.' or 'Timeout, No TPM chip found, activating TPM-bypass!'

2. <span data-ttu-id="12db7-136">Obtener la dirección IP de Hola de hello Intel NUC ejecutando hello `ifconfig` comando en el dispositivo de Intel NUC Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-136">Get hello IP address of hello Intel NUC by running hello `ifconfig` command on hello Intel NUC device.</span></span>

   <span data-ttu-id="12db7-137">Este es un ejemplo de salida del comando Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-137">Here is an example of hello command output.</span></span>

   ![Salida de ifconfig que muestra la dirección IP de Intel NUC](media/iot-hub-gateway-kit-lessons/lesson1/ifconfig.png)

   <span data-ttu-id="12db7-139">En este ejemplo, Hola valor siguiente `inet addr:` es dirección IP de Hola que necesite conectarse cuando toohello Intel NUC desde un equipo host.</span><span class="sxs-lookup"><span data-stu-id="12db7-139">In this example, hello value that follows `inet addr:` is hello IP address that you need when connect toohello Intel NUC from a host computer.</span></span>

3. <span data-ttu-id="12db7-140">Utilice uno de hello siguiendo a los clientes SSH de su tooIntel de tooconnect del equipo host NUC.</span><span class="sxs-lookup"><span data-stu-id="12db7-140">Use one of hello following SSH clients from your host computer tooconnect tooIntel NUC.</span></span>

    - <span data-ttu-id="12db7-141">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="12db7-141">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="12db7-142">cliente SSH integrado de Hello en Ubuntu o macOS.</span><span class="sxs-lookup"><span data-stu-id="12db7-142">hello built-in SSH client on Ubuntu or macOS.</span></span>

   <span data-ttu-id="12db7-143">Es más eficaz y productiva toooperate un NUC Intel desde un equipo host.</span><span class="sxs-lookup"><span data-stu-id="12db7-143">It is more efficient and productive toooperate an Intel NUC from a host computer.</span></span> <span data-ttu-id="12db7-144">Será necesario Hola dirección IP de Intel NUC, tooit tooconnect a través de un cliente de SSH del nombre y la contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="12db7-144">You'll need hello Intel NUC's IP address, user name and password tooconnect tooit via an SSH client.</span></span> <span data-ttu-id="12db7-145">Este es un ejemplo que utiliza un cliente de SSH en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="12db7-145">Here is an example that uses an SSH client on macOS.</span></span>
   <span data-ttu-id="12db7-146">![Cliente de SSH que se ejecuta en macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span><span class="sxs-lookup"><span data-stu-id="12db7-146">![SSH client running on macOS](media/iot-hub-gateway-kit-lessons/lesson1/ssh.png)</span></span>

## <a name="install-hello-azure-iot-edge-package"></a><span data-ttu-id="12db7-147">Instalar el paquete de hello borde de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="12db7-147">Install hello Azure IoT Edge package</span></span>

<span data-ttu-id="12db7-148">paquete de Hello borde de IoT de Azure contiene archivos binarios precompilados de Hola de borde de IoT y sus dependencias.</span><span class="sxs-lookup"><span data-stu-id="12db7-148">hello Azure IoT Edge package contains hello pre-compiled binaries of IoT Edge and its dependencies.</span></span> <span data-ttu-id="12db7-149">Estos archivos binarios forman borde de IoT de Azure, Hola IoT de Azure SDK y herramientas correspondientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-149">These binaries are Azure IoT Edge, hello Azure IoT SDK and hello corresponding tools.</span></span> <span data-ttu-id="12db7-150">Hello paquete también contiene una "hello_world" aplicación de ejemplo es una funcionalidad de puerta de enlace de hello toovalidate usado.</span><span class="sxs-lookup"><span data-stu-id="12db7-150">hello package also contains a "hello_world" sample application is used toovalidate hello gateway functionality.</span></span> <span data-ttu-id="12db7-151">Borde de IoT es parte del núcleo de Hola de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="12db7-151">IoT Edge is hello core part of hello gateway.</span></span> 

<span data-ttu-id="12db7-152">Siga estos paquetes de saludo de tooinstall de pasos.</span><span class="sxs-lookup"><span data-stu-id="12db7-152">Follow these steps tooinstall hello package.</span></span>

1. <span data-ttu-id="12db7-153">Agregue Hola repositorio IoT nube ejecutando Hola siga los comandos en una ventana de terminal:</span><span class="sxs-lookup"><span data-stu-id="12db7-153">Add hello IoT Cloud repository by running hello following commands in a terminal window:</span></span>

   ```bash
   rpm --import https://iotdk.intel.com/misc/iot_pub2.key
   smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
   smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
   ```

   > <span data-ttu-id="12db7-154">Escriba 'y', cuando se le pida too'Include este canal?'</span><span class="sxs-lookup"><span data-stu-id="12db7-154">Enter 'y', when it prompts you too'Include this channel?'</span></span>
   
   <span data-ttu-id="12db7-155">Si recibe un `import read failed(-1)` error, Hola de uso después de emitir de hello tooresolve de comandos:</span><span class="sxs-lookup"><span data-stu-id="12db7-155">If you receive an `import read failed(-1)` error, use hello following commands tooresolve hello issue:</span></span>
   ```bash
   wget http://iotdk.intel.com/misc/iot_pub2.key 
   rpm --import iot_pub2.key  
   ```

   <span data-ttu-id="12db7-156">Hola `rpm` comando importaciones Hola clave rpm.</span><span class="sxs-lookup"><span data-stu-id="12db7-156">hello `rpm` command imports hello rpm key.</span></span> <span data-ttu-id="12db7-157">Hola `smart channel` comando agrega rpm Hola canal toohello inteligente Administrador de paquetes.</span><span class="sxs-lookup"><span data-stu-id="12db7-157">hello `smart channel` command adds hello rpm channel toohello Smart Package Manager.</span></span> <span data-ttu-id="12db7-158">Antes de ejecutar hello `smart update` comando, verá una salida como a continuación.</span><span class="sxs-lookup"><span data-stu-id="12db7-158">Before you run hello `smart update` command, you will see an output like below.</span></span>

   ![salida de los comandos rpm y de canal inteligente](media/iot-hub-gateway-kit-lessons/lesson1/rpm_smart_channel.png)

2. <span data-ttu-id="12db7-160">Ejecutar el comando de actualización inteligente de hello:</span><span class="sxs-lookup"><span data-stu-id="12db7-160">Execute hello smart update command:</span></span>

   ```bash
   smart update
   ```

3. <span data-ttu-id="12db7-161">Instalar el paquete de puerta de enlace de IoT de Azure de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="12db7-161">Install hello Azure IoT Gateway package by running hello following command:</span></span>

   ```bash
   smart install packagegroup-cloud-azure -y
   ```

   <span data-ttu-id="12db7-162">`packagegroup-cloud-azure`es el nombre de Hola de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="12db7-162">`packagegroup-cloud-azure` is hello name of hello package.</span></span> <span data-ttu-id="12db7-163">Hola `smart install` comando es paquete de hello tooinstall usado.</span><span class="sxs-lookup"><span data-stu-id="12db7-163">hello `smart install` command is used tooinstall hello package.</span></span>

    > <span data-ttu-id="12db7-164">Siguiente ejecución Hola comando si ve este error: "clave pública no está disponible"</span><span class="sxs-lookup"><span data-stu-id="12db7-164">Run hello following command if you see this error: 'public key not available'</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```
    > <span data-ttu-id="12db7-165">Reiniciar Hola Intel NUC si ve este error: 'no hay ningún paquete proporciona util-linux-dev'</span><span class="sxs-lookup"><span data-stu-id="12db7-165">Reboot hello Intel NUC if you see this error: 'no package provides util-linux-dev'</span></span>

   <span data-ttu-id="12db7-166">Después de instalar el paquete de hello, Intel NUC es listo toofunction como una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="12db7-166">After hello package is installed, Intel NUC is ready toofunction as a gateway.</span></span>

## <a name="run-hello-azure-iot-edge-helloworld-sample-application"></a><span data-ttu-id="12db7-167">Ejecutar aplicación de ejemplo de "hello_world" hello borde de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="12db7-167">Run hello Azure IoT Edge "hello_world" sample application</span></span>

<span data-ttu-id="12db7-168">Hola tras la aplicación de ejemplo crea una puerta de enlace de un `hello_world.json` de archivos y utiliza componentes fundamentales de Hola de borde de IoT de Azure arquitectura toolog un archivo de tooa de mensaje hello world (log.txt) cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="12db7-168">hello following sample application creates a gateway from a `hello_world.json` file and uses hello fundamental components of Azure IoT Edge architecture toolog a hello world message tooa file (log.txt) every 5 seconds.</span></span>

<span data-ttu-id="12db7-169">Puede ejecutar el ejemplo de Hola a todos de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="12db7-169">You can run hello Hello World sample by executing hello following commands:</span></span>

```bash
cd /usr/share/azureiotgatewaysdk/samples/hello_world/
./hello_world hello_world.json
```

<span data-ttu-id="12db7-170">Permiten la aplicación hello World Hola ejecutar durante unos minutos y, a continuación, presionar Hola ENTRAR clave toostop se.</span><span class="sxs-lookup"><span data-stu-id="12db7-170">Let hello Hello World application run for a few minutes and then hit hello Enter key toostop it.</span></span>
<span data-ttu-id="12db7-171">![resultado de la aplicación](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span><span class="sxs-lookup"><span data-stu-id="12db7-171">![application output](media/iot-hub-gateway-kit-lessons/lesson1/hello_world.png)</span></span>

> <span data-ttu-id="12db7-172">Puede omitir los errores sobre control de argumento no válido (NULL) que aparecen tras pulsar Entrar.</span><span class="sxs-lookup"><span data-stu-id="12db7-172">You can ignore any 'invalid argument handle(NULL)' errors that appear after you hit Enter.</span></span>

<span data-ttu-id="12db7-173">Puede comprobar esa puerta de enlace de Hola se ejecutó correctamente, abra el archivo log.txt hello que se encuentra ahora en la carpeta hello_world ![log.txt vista del directorio](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span><span class="sxs-lookup"><span data-stu-id="12db7-173">You can verify that hello gateway ran successfully by opening hello log.txt file that is now in your hello_world folder ![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtdir.png)</span></span>

<span data-ttu-id="12db7-174">Abra log.txt mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="12db7-174">Open log.txt using hello following command:</span></span>

```bash
vim log.txt
```

<span data-ttu-id="12db7-175">A continuación, verá contenido Hola de log.txt, que será una salida JSON con formato de mensajes de registro de hello escritos por el módulo de Hello World de puerta de enlace de hello cada 5 segundos.</span><span class="sxs-lookup"><span data-stu-id="12db7-175">You will then see hello contents of log.txt, which will be a JSON formatted output of hello logging messages that were written every 5 seconds by hello gateway Hello World module.</span></span>
<span data-ttu-id="12db7-176">![vista de directorio de log.txt](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span><span class="sxs-lookup"><span data-stu-id="12db7-176">![log.txt directory view](media/iot-hub-gateway-kit-lessons/lesson1/logtxtview.png)</span></span>

<span data-ttu-id="12db7-177">Si tiene problemas, buscar soluciones en hello [página solución de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="12db7-177">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="summary"></a><span data-ttu-id="12db7-178">Resumen</span><span class="sxs-lookup"><span data-stu-id="12db7-178">Summary</span></span>

<span data-ttu-id="12db7-179">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="12db7-179">Congratulations!</span></span> <span data-ttu-id="12db7-180">Ha terminado de configurar Intel NUC como puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="12db7-180">You've finished setting up Intel NUC as a gateway.</span></span> <span data-ttu-id="12db7-181">Ahora está listo toomove en toohello siguiente lección tooset el equipo host, se crea un centro de IoT de Azure y registrar el dispositivo lógico de centro de IoT de Azure.</span><span class="sxs-lookup"><span data-stu-id="12db7-181">Now you're ready toomove on toohello next lesson tooset up your host computer, create an Azure IoT Hub and register your Azure IoT Hub logical device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12db7-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="12db7-182">Next steps</span></span>
[<span data-ttu-id="12db7-183">Usar un tooconnect de puerta de enlace de IoT un centro de IoT tooAzure de dispositivo</span><span class="sxs-lookup"><span data-stu-id="12db7-183">Use an IoT gateway tooconnect a device tooAzure IoT Hub</span></span>](iot-hub-gateway-kit-c-iot-gateway-connect-device-to-cloud.md)

