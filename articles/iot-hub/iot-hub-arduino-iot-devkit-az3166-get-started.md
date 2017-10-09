---
title: aaaIoT DevKit toocloud - conectar IoT DevKit AZ3166 tooAzure centro de IoT | Documentos de Microsoft
description: "Obtenga información acerca de cómo toosetup y conéctese de plataforma de nube de Azure de toosend datos toohello IoT DevKit AZ3166 tooAzure centro de IoT para él en este tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.openlocfilehash: fd36abaed1fd9f73028b84312bca9e900fb9c004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-iot-devkit-az3166-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="8c53e-103">Conectar IoT DevKit AZ3166 tooAzure centro de IoT en nube Hola</span><span class="sxs-lookup"><span data-stu-id="8c53e-103">Connect IoT DevKit AZ3166 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="8c53e-104">Hola [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) pueden ser usado toodevelop y prototipo soluciones de Internet de las cosas (IoT) aprovechan los servicios de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8c53e-104">hello [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) can be used toodevelop and prototype Internet of Things (IoT) solutions leveraging Microsoft Azure services.</span></span> <span data-ttu-id="8c53e-105">Incluye una placa compatible con Arduino con periféricos y sensores enriquecidos, un paquete de panel de código abierto y un [catálogo proyectos](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/) en aumento.</span><span class="sxs-lookup"><span data-stu-id="8c53e-105">It includes an Arduino compatible board with rich peripherals and sensors, an open-source board package and a growing [projects catalog](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8c53e-106">Qué debe hacer</span><span class="sxs-lookup"><span data-stu-id="8c53e-106">What you do</span></span>
<span data-ttu-id="8c53e-107">Conectar [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan centro de IoT de Azure que cree, Hola recopilar los datos de temperatura y humedad de sensores y enviar tooIoT concentrador de Hola de datos.</span><span class="sxs-lookup"><span data-stu-id="8c53e-107">Connect [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) tooan Azure IoT hub that you create, collect hello temperature and humidity data from sensors and send hello data tooIoT hub.</span></span>

<span data-ttu-id="8c53e-108">¿Aún no tiene un DevKit?</span><span class="sxs-lookup"><span data-stu-id="8c53e-108">Don't have a DevKit yet?</span></span> <span data-ttu-id="8c53e-109">Obtenga uno nuevo [aquí](https://aka.ms/iot-devkit-purchase).</span><span class="sxs-lookup"><span data-stu-id="8c53e-109">Get a new one [here](https://aka.ms/iot-devkit-purchase).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="8c53e-110">Conocimientos que adquirirá</span><span class="sxs-lookup"><span data-stu-id="8c53e-110">What you learn</span></span>

* <span data-ttu-id="8c53e-111">¿Cómo tooconnect IoT DevKit tooWireless acceso elija y preparar el entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-111">How tooconnect IoT DevKit tooWireless access point and prepare your development environment.</span></span>
* <span data-ttu-id="8c53e-112">¿Cómo toocreate un centro de IoT y registrar un dispositivo para MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="8c53e-112">How toocreate an IoT hub and register a device for MXChip IoT DevKit.</span></span>
* <span data-ttu-id="8c53e-113">¿Cómo toocollect datos del sensor mediante la ejecución de una aplicación de ejemplo en MXChip IoT DevKit.</span><span class="sxs-lookup"><span data-stu-id="8c53e-113">How toocollect sensor data by running a sample application on MXChip IoT DevKit.</span></span>
* <span data-ttu-id="8c53e-114">¿Cómo toosend Hola centro de IoT de tooyour de datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="8c53e-114">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8c53e-115">Lo que necesita</span><span class="sxs-lookup"><span data-stu-id="8c53e-115">What you need</span></span>

* <span data-ttu-id="8c53e-116">Una placa MXChip IoT DevKit con un cable microUSB.</span><span class="sxs-lookup"><span data-stu-id="8c53e-116">An MXChip IoT DevKit board with a micro USB cable.</span></span> [<span data-ttu-id="8c53e-117">Obténgalo ahora</span><span class="sxs-lookup"><span data-stu-id="8c53e-117">Get it now</span></span>](https://aka.ms/iot-devkit-purchase)
* <span data-ttu-id="8c53e-118">Un equipo con Windows 10 o macOS 10.10+</span><span class="sxs-lookup"><span data-stu-id="8c53e-118">A computer running Windows 10 or macOS 10.10+</span></span>
* <span data-ttu-id="8c53e-119">Una suscripción de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="8c53e-119">An active Azure subscription</span></span>
  * <span data-ttu-id="8c53e-120">Active una [cuenta de Microsoft Azure de prueba de 30 días gratis](https://azureinfo.microsoft.com/us-freetrial.html)</span><span class="sxs-lookup"><span data-stu-id="8c53e-120">Activate a [free 30-day trial Microsoft Azure account](https://azureinfo.microsoft.com/us-freetrial.html)</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="8c53e-121">Preparar el hardware</span><span class="sxs-lookup"><span data-stu-id="8c53e-121">Prepare your hardware</span></span>

<span data-ttu-id="8c53e-122">Enlazar equipo tooyour de hello hardware.</span><span class="sxs-lookup"><span data-stu-id="8c53e-122">Hook up hello hardware tooyour computer.</span></span>

### <a name="hardware-you-need"></a><span data-ttu-id="8c53e-123">Hardware que necesita</span><span class="sxs-lookup"><span data-stu-id="8c53e-123">Hardware you need</span></span>

* <span data-ttu-id="8c53e-124">Placa DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-124">DevKit board</span></span>
* <span data-ttu-id="8c53e-125">Cable microUSB</span><span class="sxs-lookup"><span data-stu-id="8c53e-125">Micro USB cable</span></span>

![getting-started-hardware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

### <a name="connect-devkit-tooyour-computer"></a><span data-ttu-id="8c53e-127">Conectar el equipo de tooyour DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-127">Connect DevKit tooyour computer</span></span>

1. <span data-ttu-id="8c53e-128">Conectar USB final tooyour PC</span><span class="sxs-lookup"><span data-stu-id="8c53e-128">Connect USB end tooyour PC</span></span>
2. <span data-ttu-id="8c53e-129">Conectar Micro USB final toohello DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-129">Connect Micro USB end toohello DevKit</span></span>
3. <span data-ttu-id="8c53e-130">Hola verde LED siguiente toopower confirma la conexión</span><span class="sxs-lookup"><span data-stu-id="8c53e-130">hello green LED next toopower confirms connection</span></span>

![getting-started-connect](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wifi"></a><span data-ttu-id="8c53e-132">Configuración de la red WiFi</span><span class="sxs-lookup"><span data-stu-id="8c53e-132">Configure WiFi</span></span>

<span data-ttu-id="8c53e-133">Los proyectos de IoT se basan en la conectividad a Internet.</span><span class="sxs-lookup"><span data-stu-id="8c53e-133">IoT projects rely on Internet connectivity.</span></span> <span data-ttu-id="8c53e-134">Usar hello siguiendo las instrucciones tooconfigure hello DevKit tooconnect tooWiFi.</span><span class="sxs-lookup"><span data-stu-id="8c53e-134">Use hello following instructions tooconfigure hello DevKit tooconnect tooWiFi.</span></span>

### <a name="enter-ap-mode"></a><span data-ttu-id="8c53e-135">Entrada al modo AP</span><span class="sxs-lookup"><span data-stu-id="8c53e-135">Enter AP Mode</span></span>

<span data-ttu-id="8c53e-136">Mantenga presionado el botón B, a continuación, insertar y suelte el botón de restablecimiento de hello y, a continuación, versión botón B. Su DevKit pasará al modo de punto de acceso para la configuración de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8c53e-136">Hold down button B, then push and release hello reset button, then release button B. Your DevKit will enter AP Mode for configuring WiFi.</span></span> <span data-ttu-id="8c53e-137">pantalla de bienvenida mostrará Hola servicio establecer Identifier(SSID) de hello DevKit, así como la dirección IP del portal de configuración de hello:</span><span class="sxs-lookup"><span data-stu-id="8c53e-137">hello screen will display hello Service Set Identifier(SSID) of hello DevKit as well as hello configuration portal IP address:</span></span>

![getting-started-wifi-ap](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-toodevkit-ap"></a><span data-ttu-id="8c53e-139">Conectar tooDevKit PA</span><span class="sxs-lookup"><span data-stu-id="8c53e-139">Connect tooDevKit AP</span></span>

<span data-ttu-id="8c53e-140">Ahora, use otro Wi-Fi habilitado dispositivos (PC o un teléfono móvil) tooconnect toohello SSID DevKit (resaltado en la captura de pantalla de hello anterior), deje Hola contraseña vacía.</span><span class="sxs-lookup"><span data-stu-id="8c53e-140">Now, use another WiFi enabled device (PC or mobile phone) tooconnect toohello DevKit SSID (highlighted in hello screenshot above), leave hello password empty.</span></span>

![getting-started-ssid](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wifi-for-devkit"></a><span data-ttu-id="8c53e-142">Configuración de la red WiFi para DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-142">Configure WiFi for DevKit</span></span>

<span data-ttu-id="8c53e-143">Dirección IP de hello abierta se muestra en la pantalla de bienvenida DevKit en su PC o el Explorador de teléfono móvil, seleccione red Wi-Fi de hello desea hello DevKit tooconnect para, a continuación, escriba Hola contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c53e-143">Open hello IP address shown on hello DevKit screen on your PC or mobile phone browser, select hello WiFi network you want hello DevKit tooconnect to, then type hello password.</span></span> <span data-ttu-id="8c53e-144">Haga clic en **conectar** toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8c53e-144">Click **Connect** toocomplete:</span></span>

![getting-started-wifi-portal](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

<span data-ttu-id="8c53e-146">Cuando se complete correctamente la conexión de hello, hello DevKit se reiniciará en unos segundos.</span><span class="sxs-lookup"><span data-stu-id="8c53e-146">Once hello connection succeeds, hello DevKit will reboot in a few seconds.</span></span> <span data-ttu-id="8c53e-147">Si se realizó correctamente, verá Hola Wi-Fi nombre y dirección IP en la pantalla de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="8c53e-147">If succeeded, you will see hello WiFi name and IP address on hello screen:</span></span>

![getting-started-wifi-ip](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
<span data-ttu-id="8c53e-149">dirección IP de Hello muestra de foto de hello no puede coincidir con hello real IP asigna y se muestran en la pantalla de bienvenida DevKit.</span><span class="sxs-lookup"><span data-stu-id="8c53e-149">hello IP address displayed in hello photo may not match hello actual IP assigned and displayed on hello DevKit screen.</span></span> <span data-ttu-id="8c53e-150">Esto es normal que utilizan Wi-Fi toodynamically DHCP asignar direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="8c53e-150">This is normal as WiFi uses DHCP toodynamically assign IPs.</span></span>

<span data-ttu-id="8c53e-151">Después de configura la red Wi-Fi, sus credenciales se conservarán en el dispositivo de Hola para esa conexión, incluso si desconectado.</span><span class="sxs-lookup"><span data-stu-id="8c53e-151">After WiFi is configured, your credentials will be persisted on hello device for that connection, even if unplugged.</span></span> <span data-ttu-id="8c53e-152">Por ejemplo, si configurado hello DevKit para Wi-Fi en su hogar y, a continuación, tardó office de hello DevKit toohello, necesitará tooreconfigure PA modo (comenzando por el paso **especificar el modo de Asia Pacífico**) hello tooconnect DevKit tooyour office Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="8c53e-152">For example, if you configured hello DevKit for WiFi in your home and then took hello DevKit toohello office, you will need tooreconfigure AP mode (starting at step **Enter AP Mode**) tooconnect hello DevKit tooyour office WiFi.</span></span> 

## <a name="start-using-devkit"></a><span data-ttu-id="8c53e-153">Uso inicial del DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-153">Start using DevKit</span></span>

<span data-ttu-id="8c53e-154">aplicación predeterminada de Hello con DevKit se compruebe Hola versión más reciente del firmware de Hola y mostrar algunos datos de diagnóstico de sensor para usted.</span><span class="sxs-lookup"><span data-stu-id="8c53e-154">hello default app running on DevKit will check hello latest version of hello firmware and display some sensor diagnosis data for you.</span></span>

### <a name="upgrade-toohello-latest-firmware"></a><span data-ttu-id="8c53e-155">Actualizar el firmware más reciente de toohello</span><span class="sxs-lookup"><span data-stu-id="8c53e-155">Upgrade toohello latest firmware</span></span>

<span data-ttu-id="8c53e-156">Se le pedirá en pantalla de bienvenida que ambos Hola versión de firmware más reciente y actual si no hay una actualización necesitada.</span><span class="sxs-lookup"><span data-stu-id="8c53e-156">You will be prompted on hello screen both hello current and latest firmware version if there is an upgrade needed.</span></span> <span data-ttu-id="8c53e-157">Siga [actualizar firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guía tooupgrade.</span><span class="sxs-lookup"><span data-stu-id="8c53e-157">Follow [Upgrade firmware](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/) guide tooupgrade it.</span></span>

![getting-started-firmware](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
<span data-ttu-id="8c53e-159">Se trata de un esfuerzo por única vez, una vez que comience el desarrollo en hello DevKit y cargar la aplicación, tendrá que firmware más reciente de hello vienen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c53e-159">This is a one-time effort, once you start developing on hello DevKit and upload your app, you will have hello latest firmware come with your app.</span></span>

### <a name="test-various-sensors"></a><span data-ttu-id="8c53e-160">Prueba de varios sensores</span><span class="sxs-lookup"><span data-stu-id="8c53e-160">Test various sensors</span></span>

<span data-ttu-id="8c53e-161">Presione sensores de tootest botón B, continúe presionando y liberar toocycle de botón Hola B a través de cada sensor.</span><span class="sxs-lookup"><span data-stu-id="8c53e-161">Press button B tootest sensors, continue pressing and releasing hello B button toocycle through each sensor.</span></span>

![getting-started-sensors](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-development-environment"></a><span data-ttu-id="8c53e-163">Preparación del entorno de desarrollo</span><span class="sxs-lookup"><span data-stu-id="8c53e-163">Prepare development environment</span></span>

<span data-ttu-id="8c53e-164">Ahora es tiempo tooset el entorno de desarrollo de hello: herramientas y paquetes para toobuild increíbles aplicaciones de IoT.</span><span class="sxs-lookup"><span data-stu-id="8c53e-164">Now it's time tooset up hello development environment: tools and packages for you toobuild stunning IoT applications.</span></span> <span data-ttu-id="8c53e-165">Puede elegir la versión de Windows o macOS según el sistema operativo de tooyour.</span><span class="sxs-lookup"><span data-stu-id="8c53e-165">You can choose Windows or macOS version according tooyour operating system.</span></span>


### <a name="windows"></a><span data-ttu-id="8c53e-166">Windows</span><span class="sxs-lookup"><span data-stu-id="8c53e-166">Windows</span></span>

<span data-ttu-id="8c53e-167">Le recomendamos toouse Hola instalación paquete tooprepare Hola entorno de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-167">We encourage you toouse hello installation package tooprepare hello development environment.</span></span> <span data-ttu-id="8c53e-168">Si tiene algún problema, puede seguir hello [requieren pasos manuales](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-168">If you encounter any issues, you can follow hello [manual steps](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/) tooget it done.</span></span>

#### <a name="download-latest-package"></a><span data-ttu-id="8c53e-169">Descarga del paquete más reciente</span><span class="sxs-lookup"><span data-stu-id="8c53e-169">Download latest package</span></span>

<span data-ttu-id="8c53e-170">Hola `.zip` descarga de archivos contiene todos los paquetes necesarios para el desarrollo de DevKit y herramientas que necesitan.</span><span class="sxs-lookup"><span data-stu-id="8c53e-170">hello `.zip` file you download contains all necessary tools and packages required for DevKit development.</span></span>

> [!div class="button"]
[<span data-ttu-id="8c53e-171">Descargar</span><span class="sxs-lookup"><span data-stu-id="8c53e-171">Download</span></span>](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


> [!NOTE] 
> <span data-ttu-id="8c53e-172">Hola `.zip` archivo contiene siguiente Hola herramientas y paquetes.</span><span class="sxs-lookup"><span data-stu-id="8c53e-172">hello `.zip` file contains hello following tools and packages.</span></span> <span data-ttu-id="8c53e-173">Si ya tiene algunos componentes instalados, el script de Hola detectará y omitirlos.</span><span class="sxs-lookup"><span data-stu-id="8c53e-173">If you already have some components installed, hello script will detect and skip them.</span></span>
> * <span data-ttu-id="8c53e-174">Node.js y Yarn: tiempo de ejecución para el script de instalación de Hola y las tareas automatizadas</span><span class="sxs-lookup"><span data-stu-id="8c53e-174">Node.js and Yarn: Runtime for hello setup script and automated tasks</span></span>
> * <span data-ttu-id="8c53e-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) -multiplataforma experiencia de línea de comandos para administrar recursos de Azure, Hola MSI contiene dependientes Python y pip.</span><span class="sxs-lookup"><span data-stu-id="8c53e-175">[Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows) - Cross-platform command-line experience for managing Azure resources, hello MSI contains dependent Python and pip.</span></span>
> * <span data-ttu-id="8c53e-176">[Visual Studio Code](https://code.visualstudio.com/): editor de código ligero para el desarrollo de DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-176">[Visual Studio Code](https://code.visualstudio.com/): Lightweight code editor for DevKit development</span></span>
> * <span data-ttu-id="8c53e-177">[Extensión de Visual Studio Code para Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): habilita el desarrollo de Arduino en Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8c53e-177">[Visual Studio Code extension for Arduino](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino): Enables Arduino development in VS Code</span></span>
> * <span data-ttu-id="8c53e-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): extensión de Hola para Arduino se basa en esta herramienta</span><span class="sxs-lookup"><span data-stu-id="8c53e-178">[Arduino IDE](https://www.arduino.cc/en/Main/Software): hello extension for Arduino relies on this tool</span></span>
> * <span data-ttu-id="8c53e-179">Paquete de placa de DevKit: Herramienta cadenas, las bibliotecas y proyectos para hello DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-179">DevKit Board Package: Tool chains, libraries and projects for hello DevKit</span></span>
> * <span data-ttu-id="8c53e-180">Utilidad ST-Link: controladores y utilidades esenciales</span><span class="sxs-lookup"><span data-stu-id="8c53e-180">ST-Link Utility: Essential utilities and drivers</span></span>

#### <a name="run-installation-script"></a><span data-ttu-id="8c53e-181">Ejecución del script de instalación</span><span class="sxs-lookup"><span data-stu-id="8c53e-181">Run installation script</span></span>

<span data-ttu-id="8c53e-182">En el Explorador de archivos de Windows, busque hello `.zip` y extraerlo, busque `install.cmd`, pulse el botón derecho y seleccione **"Ejecutar como administrador"** toostart.</span><span class="sxs-lookup"><span data-stu-id="8c53e-182">In Windows File Explorer, locate hello `.zip` and extract it, find `install.cmd`, right-click and select **"Run as administrator"** toostart.</span></span>

![getting-started-run-admin](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

<span data-ttu-id="8c53e-184">Durante la instalación, verá el progreso Hola de cada herramienta o un paquete.</span><span class="sxs-lookup"><span data-stu-id="8c53e-184">During installation, you will see hello progress of each tool or package.</span></span>

![getting-started-install](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="confirm-tooinstall-drivers"></a><span data-ttu-id="8c53e-186">Confirmar tooinstall controladores</span><span class="sxs-lookup"><span data-stu-id="8c53e-186">Confirm tooinstall drivers</span></span>

<span data-ttu-id="8c53e-187">Hola frente a código de extensión Arduino se basa en hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="8c53e-187">hello VS Code for Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="8c53e-188">Si es Hola primera vez que se va a instalar hello Arduino IDE, es posible que los controladores relevantes tooinstall solicitadas:</span><span class="sxs-lookup"><span data-stu-id="8c53e-188">If this is hello first time you are installing hello Arduino IDE, you will be prompted tooinstall relevant drivers:</span></span>

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

<span data-ttu-id="8c53e-190">Tiempo debe durar la instalación de toofinish de aproximadamente 10 minutos según la velocidad de Internet.</span><span class="sxs-lookup"><span data-stu-id="8c53e-190">It should take around 10 minutes toofinish installation depending on your Internet speed.</span></span> <span data-ttu-id="8c53e-191">Una vez completada la instalación de hello, debería ver el código de Visual Studio y Arduino IDE los métodos abreviados en el escritorio.</span><span class="sxs-lookup"><span data-stu-id="8c53e-191">Once hello installation is complete, you should see Visual Studio Code and Arduino IDE shortcuts on your desktop.</span></span>

> [!NOTE] 
<span data-ttu-id="8c53e-192">En ocasiones, al iniciar VS Code, aparece un error que indica que no se encuentra el IDE de Arduino o un paquete de la placa.</span><span class="sxs-lookup"><span data-stu-id="8c53e-192">Occasionally, when you launch VS Code, you will be prompted with an error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="8c53e-193">toosolve lo, cerrar VS Code, inicie Arduino IDE una vez y el código de VS deben buscar ruta de acceso Arduino IDE correctamente.</span><span class="sxs-lookup"><span data-stu-id="8c53e-193">toosolve it, close VS Code, launch Arduino IDE once and VS Code should locate Arduino IDE path correctly.</span></span>


### <a name="macos-preview"></a><span data-ttu-id="8c53e-194">macOS (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="8c53e-194">macOS (Preview)</span></span>

<span data-ttu-id="8c53e-195">Siga estos entorno de desarrollo de pasos tooprepare macOS.</span><span class="sxs-lookup"><span data-stu-id="8c53e-195">Follow these steps tooprepare development environment on macOS.</span></span>

#### <a name="install-azure-cli-20"></a><span data-ttu-id="8c53e-196">Instalación de la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8c53e-196">Install Azure CLI 2.0</span></span>

<span data-ttu-id="8c53e-197">Siga hello [guía oficial](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall 2.0 de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="8c53e-197">Follow hello [official guide](https://docs.microsoft.com//cli/azure/install-azure-cli) tooinstall Azure CLI 2.0:</span></span>

<span data-ttu-id="8c53e-198">Instale la CLI de Azure 2.0 con un comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="8c53e-198">Install Azure CLI 2.0 with one `curl` command:</span></span>

```bash
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="8c53e-199">Y reiniciar el shell de comandos para cambios tootake efecto:</span><span class="sxs-lookup"><span data-stu-id="8c53e-199">And restart your command shell for changes tootake effect:</span></span>

```bash
exec -l $SHELL
```

#### <a name="install-arduino-ide"></a><span data-ttu-id="8c53e-200">Instalación del IDE de Arduino</span><span class="sxs-lookup"><span data-stu-id="8c53e-200">Install Arduino IDE</span></span>

<span data-ttu-id="8c53e-201">Hola extensión Arduino de código de Visual Studio se basa en hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="8c53e-201">hello Visual Studio Code Arduino extension relies on hello Arduino IDE.</span></span> <span data-ttu-id="8c53e-202">Descargue e instale hello [Arduino IDE para macOS](https://www.arduino.cc/en/Main/Software).</span><span class="sxs-lookup"><span data-stu-id="8c53e-202">Download and install hello [Arduino IDE for macOS](https://www.arduino.cc/en/Main/Software).</span></span>

#### <a name="install-visual-studio-code"></a><span data-ttu-id="8c53e-203">Instalación de Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8c53e-203">Install Visual Studio Code</span></span>

<span data-ttu-id="8c53e-204">Descargue e instale [Visual Studio Code para macOS](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8c53e-204">Download and install [Visual Studio Code for macOS](https://code.visualstudio.com/).</span></span> <span data-ttu-id="8c53e-205">Se trata de hello principal herramienta de desarrollo para crear aplicaciones de DevKit IoT.</span><span class="sxs-lookup"><span data-stu-id="8c53e-205">This will be hello primary development tool for building DevKit IoT applications.</span></span>

####  <a name="download-latest-package"></a><span data-ttu-id="8c53e-206">Descarga del paquete más reciente</span><span class="sxs-lookup"><span data-stu-id="8c53e-206">Download latest package</span></span>

1. <span data-ttu-id="8c53e-207">Instale Node.js.</span><span class="sxs-lookup"><span data-stu-id="8c53e-207">Install Node.js.</span></span> <span data-ttu-id="8c53e-208">Puede usar el Administrador de paquetes populares macOS [Homebrew](https://brew.sh/) o [pregeneradas instalador](https://nodejs.org/en/download/) tooinstall lo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-208">You can use popular macOS package manager [Homebrew](https://brew.sh/) or [pre-built installer](https://nodejs.org/en/download/) tooinstall it.</span></span>

2. <span data-ttu-id="8c53e-209">Descargue el archivo `.zip` con los scripts de tarea necesarios para el desarrollo del DevKit en VS Code.</span><span class="sxs-lookup"><span data-stu-id="8c53e-209">Download `.zip` file containing task scripts required for DevKit development in VS Code.</span></span>

   > [!div class="button"]
   [<span data-ttu-id="8c53e-210">Descargar</span><span class="sxs-lookup"><span data-stu-id="8c53e-210">Download</span></span>](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

   <span data-ttu-id="8c53e-211">Busque hello `.zip` y extráigalo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-211">Locate hello `.zip` and extract it.</span></span> <span data-ttu-id="8c53e-212">A continuación, inicie **Terminal** hello ejecución sigue tooconfigure de comandos y aplicación:</span><span class="sxs-lookup"><span data-stu-id="8c53e-212">Then launch **Terminal** app and run hello following commands tooconfigure:</span></span>

   <span data-ttu-id="8c53e-213">Mover la carpeta de usuario de la carpeta extraída tooyour macOS:</span><span class="sxs-lookup"><span data-stu-id="8c53e-213">Move extracted folder tooyour macOS user folder:</span></span>
   ```bash
   mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
   ```
  
   <span data-ttu-id="8c53e-214">Instale los paquetes `npm`:</span><span class="sxs-lookup"><span data-stu-id="8c53e-214">Install `npm` packages:</span></span>
   ```
   npm install
   ```

#### <a name="install-vs-code-extension-for-arduino"></a><span data-ttu-id="8c53e-215">Instalación de la extensión de VS Code para Arduino</span><span class="sxs-lookup"><span data-stu-id="8c53e-215">Install VS Code extension for Arduino</span></span>

<span data-ttu-id="8c53e-216">Código de Visual Studio permite extensiones de Marketplace de tooinstall directamente en la herramienta de hello, simplemente haga clic en el icono de extensiones de hello en el panel del menú izquierdo hello y, a continuación, buscar `Arduino` tooinstall:</span><span class="sxs-lookup"><span data-stu-id="8c53e-216">Visual Studio Code allows you tooinstall Marketplace extensions directly in hello tool, simply click hello extensions icon in hello left menu pane and then search `Arduino` tooinstall:</span></span>

![installation-extensions](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-devkit-board-package"></a><span data-ttu-id="8c53e-218">Instalación del paquete de la placa DevKit</span><span class="sxs-lookup"><span data-stu-id="8c53e-218">Install DevKit board package</span></span>

<span data-ttu-id="8c53e-219">Necesitará placa de DevKit de hello tooadd utilizando Hola Administrador de panel en el código de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c53e-219">You will need tooadd hello DevKit board using hello Board Manager in Visual Studio Code.</span></span>

1. <span data-ttu-id="8c53e-220">Use `Cmd+Shift+P` tooinvoke comando paleta y escriba **Arduino** , a continuación, busque y seleccione **Arduino: Administrador de panel**.</span><span class="sxs-lookup"><span data-stu-id="8c53e-220">Use `Cmd+Shift+P` tooinvoke command palette and type **Arduino** then find and select **Arduino: Board Manager**.</span></span>

2. <span data-ttu-id="8c53e-221">Haga clic en **'Las direcciones URL adicionales'** en la parte inferior de hello derecha.</span><span class="sxs-lookup"><span data-stu-id="8c53e-221">Click **'Additional URLs'** at hello bottom right.</span></span>
   <span data-ttu-id="8c53e-222">![instalación-url-adicionales](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span><span class="sxs-lookup"><span data-stu-id="8c53e-222">![installation-additional-urls](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)</span></span>

3. <span data-ttu-id="8c53e-223">Hola `settings.json` , agregue una línea en la parte inferior de Hola de `USER SETTINGS` panel y guardar.</span><span class="sxs-lookup"><span data-stu-id="8c53e-223">In hello `settings.json` file, add a line at hello bottom of `USER SETTINGS` pane and save.</span></span>
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![installation-settings-json](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. <span data-ttu-id="8c53e-225">Ahora Hola panel administrador buscar 'az3166' e instalar la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c53e-225">Now in hello Board Manager search for 'az3166' and install hello latest version.</span></span>
   <span data-ttu-id="8c53e-226">![instalación-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span><span class="sxs-lookup"><span data-stu-id="8c53e-226">![installation-az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)</span></span>

<span data-ttu-id="8c53e-227">Ahora dispone de todas las herramientas que necesitan hello y paquetes instalados para macOS.</span><span class="sxs-lookup"><span data-stu-id="8c53e-227">You now have all hello necessary tools and packages installed for macOS.</span></span>


## <a name="open-project-folder"></a><span data-ttu-id="8c53e-228">Apertura de la carpeta del proyecto</span><span class="sxs-lookup"><span data-stu-id="8c53e-228">Open project folder</span></span>

### <a name="launch-vs-code"></a><span data-ttu-id="8c53e-229">Ejecutar VS Code</span><span class="sxs-lookup"><span data-stu-id="8c53e-229">Launch VS Code</span></span>

<span data-ttu-id="8c53e-230">Asegúrese de que el DevKit no está conectado.</span><span class="sxs-lookup"><span data-stu-id="8c53e-230">Make sure your DevKit is not connected.</span></span> <span data-ttu-id="8c53e-231">Ejecutar código de VS en primer lugar y conectar hello DevKit tooyour equipo.</span><span class="sxs-lookup"><span data-stu-id="8c53e-231">Launch VS Code first and connect hello DevKit tooyour computer.</span></span> <span data-ttu-id="8c53e-232">VS Code lo encontrará automáticamente y abrirá una página de introducción emergente:</span><span class="sxs-lookup"><span data-stu-id="8c53e-232">VS Code will automatically find it and pop up an introduction page:</span></span>

![mini-solution-vscode](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
<span data-ttu-id="8c53e-234">En ocasiones, al iniciar VS Code, aparece un error que indica que no se encuentra el IDE de Arduino o un paquete de la placa.</span><span class="sxs-lookup"><span data-stu-id="8c53e-234">Occasionally, when you launch VS Code, you will be prompted with error that cannot find Arduino IDE or related board package.</span></span> <span data-ttu-id="8c53e-235">toosolve lo, cerrar VS Code, vuelva a iniciar el Arduino IDE una vez y el código de VS deben buscar ruta de acceso Arduino IDE correctamente.</span><span class="sxs-lookup"><span data-stu-id="8c53e-235">toosolve it, close VS Code, launch Arduino IDE once again and VS Code should locate Arduino IDE path correctly.</span></span>

### <a name="open-arduino-examples-folder"></a><span data-ttu-id="8c53e-236">Apertura de la carpeta de ejemplos de Arduino</span><span class="sxs-lookup"><span data-stu-id="8c53e-236">Open Arduino Examples folder</span></span>

<span data-ttu-id="8c53e-237">Cambiar demasiado**'Arduino ejemplos'** ficha, navegue demasiado`Examples for MXCHIP AZ3166 > AzureIoT` y haga clic en `GetStarted`.</span><span class="sxs-lookup"><span data-stu-id="8c53e-237">Switch too**'Arduino Examples'** tab, navigate too`Examples for MXCHIP AZ3166 > AzureIoT` and click on `GetStarted`.</span></span>

![mini-solution-examples](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

<span data-ttu-id="8c53e-239">Si se encontrara tooclose panel de hello, tooreload lo, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta y el tipo de comando tooinvoke **Arduino** toofind y seleccione **Arduino: ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="8c53e-239">If you happen tooclose hello pane, tooreload it, use `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** toofind and select **Arduino: Examples**.</span></span>

## <a name="provision-azure-services"></a><span data-ttu-id="8c53e-240">Aprovisionamiento de los servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="8c53e-240">Provision Azure services</span></span>

<span data-ttu-id="8c53e-241">En la ventana de la solución de hello, ejecute la tarea a través de `Ctrl+P` (macOS: `Cmd+P`) escribiendo 'en la nube el aprovisionamiento de tarea':</span><span class="sxs-lookup"><span data-stu-id="8c53e-241">In hello solution window, run your task through `Ctrl+P` (macOS: `Cmd+P`) by typing 'task cloud-provision':</span></span>

<span data-ttu-id="8c53e-242">Hola VS Code terminal, que una línea de comandos interactiva le guiará Hola aprovisionamiento requiere servicios de Azure:</span><span class="sxs-lookup"><span data-stu-id="8c53e-242">In hello VS Code terminal, an interactive command line will guide you through provisioning hello required Azure services:</span></span>

![mini-solution-cloud-provision](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-arduino-sketch"></a><span data-ttu-id="8c53e-244">Creación y carga del boceto de Arduino</span><span class="sxs-lookup"><span data-stu-id="8c53e-244">Build and upload Arduino sketch</span></span>

### <a name="install-required-library"></a><span data-ttu-id="8c53e-245">Instalación de la biblioteca necesaria</span><span class="sxs-lookup"><span data-stu-id="8c53e-245">Install required library</span></span>

1. <span data-ttu-id="8c53e-246">Presione `F1` o `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) paleta y el tipo de comando tooinvoke **Arduino** , a continuación, busque y seleccione **Arduino: Administrador de bibliotecas de**.</span><span class="sxs-lookup"><span data-stu-id="8c53e-246">Press `F1` or `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) tooinvoke command palette and type **Arduino** then find and select **Arduino: Library Manager**.</span></span>

2. <span data-ttu-id="8c53e-247">Busque la biblioteca `ArduinoJson` y haga clic en **Install** (Instalar)</span><span class="sxs-lookup"><span data-stu-id="8c53e-247">Search for `ArduinoJson` library and click **Install**</span></span>

### <a name="build-and-upload-hello-device-code"></a><span data-ttu-id="8c53e-248">Crear y cargar el código de dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="8c53e-248">Build and upload hello device code</span></span>

<span data-ttu-id="8c53e-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'dispositivo de tarea de carga'.</span><span class="sxs-lookup"><span data-stu-id="8c53e-249">Use `Ctrl+P` (macOS: `Cmd+P`) toorun 'task device-upload'.</span></span> <span data-ttu-id="8c53e-250">Hola terminal le pedirá tooenter el modo de configuración.</span><span class="sxs-lookup"><span data-stu-id="8c53e-250">hello terminal will prompt you tooenter configuration mode.</span></span> <span data-ttu-id="8c53e-251">toodo por lo tanto, mantenga presionado el botón A, a continuación, botón de restablecimiento de Hola de inserción y de lanzamiento.</span><span class="sxs-lookup"><span data-stu-id="8c53e-251">toodo so, hold down button A, then push and release hello reset button.</span></span> <span data-ttu-id="8c53e-252">pantalla de bienvenida mostrará "Configuración".</span><span class="sxs-lookup"><span data-stu-id="8c53e-252">hello screen will display 'Configuration'.</span></span> <span data-ttu-id="8c53e-253">Se trata de una cadena de conexión de hello tooset que recupera del paso 'aprovisionamiento en la nube de tarea'.</span><span class="sxs-lookup"><span data-stu-id="8c53e-253">This is tooset hello connection string that retrieves from 'task cloud-provision' step.</span></span>

<span data-ttu-id="8c53e-254">A continuación, se iniciará comprobando y cargando boceto de Hola Arduino:</span><span class="sxs-lookup"><span data-stu-id="8c53e-254">Then it will start verifying and uploading hello Arduino sketch:</span></span>

![mini-solution-device-upload](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

<span data-ttu-id="8c53e-256">Hola DevKit se reinicie e iniciar la ejecución de código de hello.</span><span class="sxs-lookup"><span data-stu-id="8c53e-256">hello DevKit will reboot and start running hello code.</span></span>

## <a name="test-hello-project"></a><span data-ttu-id="8c53e-257">Proyecto de prueba de Hola</span><span class="sxs-lookup"><span data-stu-id="8c53e-257">Test hello project</span></span>

<span data-ttu-id="8c53e-258">En VS Code, haga clic en el icono de plug de energía de hello en barra tooopen Hola serie Monitor de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c53e-258">In VS Code, click hello power plug icon on hello status bar tooopen hello Serial Monitor.</span></span>

<span data-ttu-id="8c53e-259">aplicación de ejemplo de Hola se esté ejecutando correctamente cuando vea Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="8c53e-259">hello sample application is running successfully when you see hello following results:</span></span>

* <span data-ttu-id="8c53e-260">Hello muestra Monitor serie Hola misma información como contenido Hola Hola captura de pantalla siguiente.</span><span class="sxs-lookup"><span data-stu-id="8c53e-260">hello Serial Monitor displays hello same information as hello content in hello screenshot below.</span></span>
* <span data-ttu-id="8c53e-261">Hola LED en MXChip IoT DevKit parpadea.</span><span class="sxs-lookup"><span data-stu-id="8c53e-261">hello LED on MXChip IoT DevKit is blinking.</span></span>

![Salida final en VS Code](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a><span data-ttu-id="8c53e-263">Problemas y comentarios</span><span class="sxs-lookup"><span data-stu-id="8c53e-263">Problems and feedback</span></span>

<span data-ttu-id="8c53e-264">Puede encontrar [preguntas más frecuentes](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) si tiene problemas o llegar toous de los canales de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="8c53e-264">You can find [FAQs](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/) if you encounter problems or reach out toous from hello channels below.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c53e-265">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c53e-265">Next steps</span></span>

<span data-ttu-id="8c53e-266">Se ha conectado correctamente un tooyour MXChip IoT DevKit centro de IoT y enviado Hola captura centro de IoT de tooyour de datos de sensor.</span><span class="sxs-lookup"><span data-stu-id="8c53e-266">You have successfully connected an MXChip IoT DevKit tooyour IoT Hub, and sent hello captured sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="8c53e-267">toocontinue introducción con el centro de IoT y tooexplore otros escenarios de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="8c53e-267">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

- [<span data-ttu-id="8c53e-268">Administración de la mensajería de dispositivos en la nube con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="8c53e-268">Manage cloud device messaging with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [<span data-ttu-id="8c53e-269">Guardar mensajes de centro de IoT tooAzure el almacenamiento de datos</span><span class="sxs-lookup"><span data-stu-id="8c53e-269">Save IoT Hub messages tooAzure data storage</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [<span data-ttu-id="8c53e-270">Utilizar datos de detección en tiempo real de Power BI toovisualize desde el centro de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="8c53e-270">Use Power BI toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [<span data-ttu-id="8c53e-271">Utilizar datos de detección en tiempo real de aplicaciones Web de Azure toovisualize desde el centro de IoT de Azure</span><span class="sxs-lookup"><span data-stu-id="8c53e-271">Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub</span></span>](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [<span data-ttu-id="8c53e-272">Boletín meteorológico utilizando los datos de sensor de Hola desde el centro de IoT en aprendizaje automático de Azure</span><span class="sxs-lookup"><span data-stu-id="8c53e-272">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [<span data-ttu-id="8c53e-273">Administración de dispositivos con iothub-explorer</span><span class="sxs-lookup"><span data-stu-id="8c53e-273">Device management with iothub-explorer</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [<span data-ttu-id="8c53e-274">Supervisión remota y notificaciones con Logic Apps</span><span class="sxs-lookup"><span data-stu-id="8c53e-274">Remote monitoring and notifications with Logic Apps</span></span>](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)