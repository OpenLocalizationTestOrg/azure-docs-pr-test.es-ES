---
title: "aaaUse un dispositivo físico con borde de IoT de Azure | Documentos de Microsoft"
description: "¿Cómo toouse un centro de IoT Texas instrumentos SensorTag dispositivo toosend datos tooan a través de una puerta de enlace de IoT borde ejecutando en un dispositivo de frambuesa Pi 3. puerta de enlace de Hola se basa en el borde de IoT de Azure."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="09873-104">Usar Azure IoT arista en un tooIoT de mensajes del dispositivo a la nube de frambuesa Pi tooforward concentrador</span><span class="sxs-lookup"><span data-stu-id="09873-104">Use Azure IoT Edge on a Raspberry Pi tooforward device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="09873-105">En este tutorial de hello [ejemplo de baja energía Bluetooth] [ lnk-ble-samplecode] muestra cómo toouse [Azure IoT borde] [ lnk-sdk] para:</span><span class="sxs-lookup"><span data-stu-id="09873-105">This walkthrough of hello [Bluetooth low energy sample][lnk-ble-samplecode] shows you how toouse [Azure IoT Edge][lnk-sdk] to:</span></span>

* <span data-ttu-id="09873-106">Reenviar tooIoT concentrador de telemetría de dispositivo para la nube desde un dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="09873-106">Forward device-to-cloud telemetry tooIoT Hub from a physical device.</span></span>
* <span data-ttu-id="09873-107">Comandos de la ruta de dispositivo físico de centro de IoT tooa.</span><span class="sxs-lookup"><span data-stu-id="09873-107">Route commands from IoT Hub tooa physical device.</span></span>

<span data-ttu-id="09873-108">En este tutorial, se describen los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="09873-108">This walkthrough covers:</span></span>

* <span data-ttu-id="09873-109">**Arquitectura**: información de arquitectura importante acerca de los ejemplos de hello Bluetooth baja energía.</span><span class="sxs-lookup"><span data-stu-id="09873-109">**Architecture**: important architectural information about hello Bluetooth low energy sample.</span></span>
* <span data-ttu-id="09873-110">**Compile y ejecute**: Hola pasos necesarios toobuild y ejemplo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="09873-110">**Build and run**: hello steps required toobuild and run hello sample.</span></span>

## <a name="architecture"></a><span data-ttu-id="09873-111">Arquitectura</span><span class="sxs-lookup"><span data-stu-id="09873-111">Architecture</span></span>

<span data-ttu-id="09873-112">Hola tutorial muestra cómo toobuild y ejecutar una puerta de enlace de IoT borde con frambuesa Pi 3 que ejecuta Raspbian Linux.</span><span class="sxs-lookup"><span data-stu-id="09873-112">hello walkthrough shows you how toobuild and run an IoT Edge gateway on a Raspberry Pi 3 that runs Raspbian Linux.</span></span> <span data-ttu-id="09873-113">puerta de enlace de Hola se basa en el borde de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-113">hello gateway is built using IoT Edge.</span></span> <span data-ttu-id="09873-114">ejemplo de Hola usa una Texas instrumentos SensorTag Bluetooth baja energía (n) dispositivo toocollect temperatura de datos.</span><span class="sxs-lookup"><span data-stu-id="09873-114">hello sample uses a Texas Instruments SensorTag Bluetooth Low Energy (BLE) device toocollect temperature data.</span></span>

<span data-ttu-id="09873-115">Cuando ejecute hello puerta de enlace de IoT borde:</span><span class="sxs-lookup"><span data-stu-id="09873-115">When you run hello IoT Edge gateway it:</span></span>

* <span data-ttu-id="09873-116">Conecta tooa SensorTag dispositivo mediante Protocolo de hello Bluetooth baja energía (n).</span><span class="sxs-lookup"><span data-stu-id="09873-116">Connects tooa SensorTag device using hello Bluetooth Low Energy (BLE) protocol.</span></span>
* <span data-ttu-id="09873-117">Se conecta tooIoT concentrador mediante Protocolo de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="09873-117">Connects tooIoT Hub using hello HTTP protocol.</span></span>
* <span data-ttu-id="09873-118">Reenvía la telemetría de hello SensorTag dispositivo tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="09873-118">Forwards telemetry from hello SensorTag device tooIoT Hub.</span></span>
* <span data-ttu-id="09873-119">Enruta los comandos de dispositivo de centro de IoT toohello SensorTag.</span><span class="sxs-lookup"><span data-stu-id="09873-119">Routes commands from IoT Hub toohello SensorTag device.</span></span>

<span data-ttu-id="09873-120">puerta de enlace de Hello contiene Hola después módulos IoT borde:</span><span class="sxs-lookup"><span data-stu-id="09873-120">hello gateway contains hello following IoT Edge modules:</span></span>

* <span data-ttu-id="09873-121">A *módulo Bilitar* que interactúa con una Bilitar dispositivo tooreceive temperatura de datos del dispositivo de Hola y enviar comandos toohello.</span><span class="sxs-lookup"><span data-stu-id="09873-121">A *BLE module* that interfaces with a BLE device tooreceive temperature data from hello device and send commands toohello device.</span></span>
* <span data-ttu-id="09873-122">A *módulo de Bilitar nube toodevice* que convierte los mensajes JSON enviados desde el centro de IoT en las instrucciones de BLE de Hola *módulo Bilitar*.</span><span class="sxs-lookup"><span data-stu-id="09873-122">A *BLE cloud toodevice module* that translates JSON messages sent from IoT Hub into BLE instructions for hello *BLE module*.</span></span>
* <span data-ttu-id="09873-123">A *módulo registrador* que registra todos los archivos locales de puerta de enlace mensajes tooa.</span><span class="sxs-lookup"><span data-stu-id="09873-123">A *logger module* that logs all gateway messages tooa local file.</span></span>
* <span data-ttu-id="09873-124">Un *módulo de asignación de identidad* que traduce entre direcciones MAC de los dispositivos BLE y las identidades de los dispositivos de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09873-124">An *identity mapping module* that translates between BLE device MAC addresses and Azure IoT Hub device identities.</span></span>
* <span data-ttu-id="09873-125">Un *módulo Centro de IoT* que carga centro de IoT de tooan de datos de telemetría y recibe los comandos de dispositivo de un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-125">An *IoT Hub module* that uploads telemetry data tooan IoT hub and receives device commands from an IoT hub.</span></span>
* <span data-ttu-id="09873-126">A *módulo de impresora Bilitar* que interprete la telemetría de dispositivo de hello Bilitar e imprime datos con formato toohello consola tooenable problemas y depuración.</span><span class="sxs-lookup"><span data-stu-id="09873-126">A *BLE printer module* that interprets telemetry from hello BLE device and prints formatted data toohello console tooenable troubleshooting and debugging.</span></span>

### <a name="how-data-flows-through-hello-gateway"></a><span data-ttu-id="09873-127">Cómo fluyen los datos a través de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="09873-127">How data flows through hello gateway</span></span>

<span data-ttu-id="09873-128">Hello después de diagrama de bloques muestra la canalización de flujo de datos de carga de telemetría de hello:</span><span class="sxs-lookup"><span data-stu-id="09873-128">hello following block diagram illustrates hello telemetry upload data flow pipeline:</span></span>

![Canalización de puerta de enlace de carga de telemetría](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

<span data-ttu-id="09873-130">pasos de Hola que un elemento de telemetría toma desplazan desde un tooIoT de dispositivo Bilitar concentrador son:</span><span class="sxs-lookup"><span data-stu-id="09873-130">hello steps that an item of telemetry takes traveling from a BLE device tooIoT Hub are:</span></span>

1. <span data-ttu-id="09873-131">dispositivo de Hello Bilitar genera una muestra de temperatura y lo envía a través del módulo de Bluetooth toohello BLE en puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-131">hello BLE device generates a temperature sample and sends it over Bluetooth toohello BLE module in hello gateway.</span></span>
1. <span data-ttu-id="09873-132">módulo BLE de Hello recibe el ejemplo hello y publica a broker toohello junto con la dirección MAC de hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-132">hello BLE module receives hello sample and publishes it toohello broker along with hello MAC address of hello device.</span></span>
1. <span data-ttu-id="09873-133">módulo de asignación de identidad de Hello toma este mensaje y utiliza un Hola de tootranslate tabla interna dirección MAC del dispositivo de hello en una identidad de dispositivo del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-133">hello identity mapping module picks up this message and uses an internal table tootranslate hello MAC address of hello device into an IoT Hub device identity.</span></span> <span data-ttu-id="09873-134">Una identidad de dispositivo de IoT Hub consta de un identificador de dispositivo y una clave de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="09873-134">An IoT Hub device identity consists of a device ID and device key.</span></span>
1. <span data-ttu-id="09873-135">módulo de asignación de identidad de Hello publica un mensaje nuevo que contiene datos de ejemplo de Hola temperatura, dirección MAC de hello de dispositivo de hello, Id. de dispositivo de Hola y clave de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-135">hello identity mapping module publishes a new message that contains hello temperature sample data, hello MAC address of hello device, hello device ID, and hello device key.</span></span>
1. <span data-ttu-id="09873-136">Hola módulo Centro de IoT recibe este mensaje nuevo (generado por el módulo de asignación de identidad de hello) y lo publica tooIoT concentrador.</span><span class="sxs-lookup"><span data-stu-id="09873-136">hello IoT Hub module receives this new message (generated by hello identity mapping module) and publishes it tooIoT Hub.</span></span>
1. <span data-ttu-id="09873-137">módulo de registrador Hola registra todos los mensajes de archivo local de hello broker tooa.</span><span class="sxs-lookup"><span data-stu-id="09873-137">hello logger module logs all messages from hello broker tooa local file.</span></span>

<span data-ttu-id="09873-138">Hello después de diagrama de bloques muestra la canalización de flujo de datos de hello dispositivo comandos:</span><span class="sxs-lookup"><span data-stu-id="09873-138">hello following block diagram illustrates hello device command data flow pipeline:</span></span>

![Canalización de puerta de enlace de comandos de dispositivo](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. <span data-ttu-id="09873-140">Hola módulo sondea periódicamente el centro de IoT Hola centro de IoT para nuevos mensajes de comando.</span><span class="sxs-lookup"><span data-stu-id="09873-140">hello IoT Hub module periodically polls hello IoT hub for new command messages.</span></span>
1. <span data-ttu-id="09873-141">Cuando Hola módulo Centro de IoT recibe un nuevo mensaje de comando, publica a toohello broker.</span><span class="sxs-lookup"><span data-stu-id="09873-141">When hello IoT Hub module receives a new command message, it publishes it toohello broker.</span></span>
1. <span data-ttu-id="09873-142">módulo de asignación de identidad de Hello recoge el mensaje de bienvenida de comando y usa un Hola de tabla interna tootranslate dispositivo de tooa de Id. de dispositivo de centro de IoT dirección MAC.</span><span class="sxs-lookup"><span data-stu-id="09873-142">hello identity mapping module picks up hello command message and uses an internal table tootranslate hello IoT Hub device ID tooa device MAC address.</span></span> <span data-ttu-id="09873-143">A continuación, publica un mensaje nuevo que incluye la dirección MAC de hello de dispositivo de destino de hello en mapa de propiedades de hello del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="09873-143">It then publishes a new message that includes hello MAC address of hello target device in hello properties map of hello message.</span></span>
1. <span data-ttu-id="09873-144">módulo BLE en la nube al dispositivo de Hello toma este mensaje y lo convierte en la instrucción de Bilitar apropiado hello para el módulo de Bilitar Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-144">hello BLE Cloud-to-Device module picks up this message and translates it into hello proper BLE instruction for hello BLE module.</span></span> <span data-ttu-id="09873-145">Luego publica un mensaje nuevo.</span><span class="sxs-lookup"><span data-stu-id="09873-145">It then publishes a new message.</span></span>
1. <span data-ttu-id="09873-146">módulo BLE de Hello toma este mensaje y ejecuta la instrucción de E/S de hello mediante la comunicación con dispositivos de Bilitar Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-146">hello BLE module picks up this message and executes hello I/O instruction by communicating with hello BLE device.</span></span>
1. <span data-ttu-id="09873-147">módulo de registrador Hola registra todos los mensajes de archivo de disco de hello broker tooa.</span><span class="sxs-lookup"><span data-stu-id="09873-147">hello logger module logs all messages from hello broker tooa disk file.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09873-148">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="09873-148">Prerequisites</span></span>

<span data-ttu-id="09873-149">toocomplete este tutorial, necesita una suscripción activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="09873-149">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="09873-150">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="09873-150">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="09873-151">Para más información, consulte la [evaluación gratuita de Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="09873-151">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

<span data-ttu-id="09873-152">Se necesita al cliente SSH en su tooenable de máquina de escritorio tooremotely acceso Hola la línea de comandos en hello frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="09873-152">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="09873-153">Windows no incluye ningún cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="09873-153">Windows does not include an SSH client.</span></span> <span data-ttu-id="09873-154">Se recomienda usar [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="09873-154">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="09873-155">La mayoría de las distribuciones de Linux y Mac OS incluyen la utilidad SSH de línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-155">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="09873-156">Para más información, consulte [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (SSH cuando se usa Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="09873-156">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

## <a name="prepare-your-hardware"></a><span data-ttu-id="09873-157">Preparar el hardware</span><span class="sxs-lookup"><span data-stu-id="09873-157">Prepare your hardware</span></span>

<span data-ttu-id="09873-158">Este tutorial se supone que usa un [SensorTag de instrumentos Texas](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) dispositivo conectado tooa frambuesa Pi 3 ejecutando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="09873-158">This tutorial assumes you are using a [Texas Instruments SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) device connected tooa Raspberry Pi 3 running Raspbian.</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="09873-159">Instalación de Raspbian</span><span class="sxs-lookup"><span data-stu-id="09873-159">Install Raspbian</span></span>

<span data-ttu-id="09873-160">Puede utilizar cualquiera de hello después opciones tooinstall Raspbian en el dispositivo de frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="09873-160">You can use either of hello following options tooinstall Raspbian on your Raspberry Pi 3 device.</span></span>

* <span data-ttu-id="09873-161">versión más reciente de hello tooinstall de Raspbian, use hello [NOOBS] [ lnk-noobs] interfaz gráfica de usuario.</span><span class="sxs-lookup"><span data-stu-id="09873-161">tooinstall hello latest version of Raspbian, use hello [NOOBS][lnk-noobs] graphical user interface.</span></span>
* <span data-ttu-id="09873-162">Manualmente [descargar] [ lnk-raspbian] y escribir la imagen más reciente de Hola de tarjeta de hello Raspbian sistema operativo tooan SD.</span><span class="sxs-lookup"><span data-stu-id="09873-162">Manually [download][lnk-raspbian] and write hello latest image of hello Raspbian operating system tooan SD card.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="09873-163">Inicio de sesión y terminal Hola</span><span class="sxs-lookup"><span data-stu-id="09873-163">Sign in and access hello terminal</span></span>

<span data-ttu-id="09873-164">Tiene dos tooaccess de opciones un entorno de terminal en su Pi frambuesa:</span><span class="sxs-lookup"><span data-stu-id="09873-164">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

* <span data-ttu-id="09873-165">Si tiene un teclado y supervisar tooyour conectado frambuesa Pi, puede usar hello Raspbian GUI tooaccess una ventana de terminal.</span><span class="sxs-lookup"><span data-stu-id="09873-165">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

* <span data-ttu-id="09873-166">Línea de comandos de acceso hello en el instalador de plataforma de frambuesa mediante SSH desde el equipo de escritorio.</span><span class="sxs-lookup"><span data-stu-id="09873-166">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="09873-167">Usar una ventana de terminal en hello GUI</span><span class="sxs-lookup"><span data-stu-id="09873-167">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="09873-168">las credenciales predeterminadas de Hola para Raspbian son nombre de usuario **pi** y la contraseña **frambuesa**.</span><span class="sxs-lookup"><span data-stu-id="09873-168">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="09873-169">En la barra de tareas de Hola Hola GUI, puede iniciar hello **Terminal** utilidad mediante el icono de Hola que parece un monitor.</span><span class="sxs-lookup"><span data-stu-id="09873-169">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="09873-170">Inicio de sesión con SSH</span><span class="sxs-lookup"><span data-stu-id="09873-170">Sign in with SSH</span></span>

<span data-ttu-id="09873-171">Puede utilizar SSH para acceso de línea de comandos tooyour frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="09873-171">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="09873-172">artículo de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] describe cómo tooconfigure SSH en el instalador de plataforma de frambuesa y cómo tooconnect de [Windows] [ lnk-ssh-windows] o [Linux y Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="09873-172">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="09873-173">Inicie sesión con el nombre de usuario **pi** y la contraseña **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="09873-173">Sign in with username **pi** and password **raspberry**.</span></span>

### <a name="install-bluez-537"></a><span data-ttu-id="09873-174">Instalación de BlueZ 5.37</span><span class="sxs-lookup"><span data-stu-id="09873-174">Install BlueZ 5.37</span></span>

<span data-ttu-id="09873-175">módulos de Hello Bilitar hable toohello Bluetooth hardware a través de la pila de BlueZ Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-175">hello BLE modules talk toohello Bluetooth hardware via hello BlueZ stack.</span></span> <span data-ttu-id="09873-176">Necesita la versión 5.37 de BlueZ para hello módulos toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="09873-176">You need version 5.37 of BlueZ for hello modules toowork correctly.</span></span> <span data-ttu-id="09873-177">Estas instrucciones Asegúrese de que está instalada la versión correcta de Hola de BlueZ.</span><span class="sxs-lookup"><span data-stu-id="09873-177">These instructions make sure hello correct version of BlueZ is installed.</span></span>

1. <span data-ttu-id="09873-178">Detener el demonio de hello actual bluetooth:</span><span class="sxs-lookup"><span data-stu-id="09873-178">Stop hello current bluetooth daemon:</span></span>

    ```sh
    sudo systemctl stop bluetooth
    ```

1. <span data-ttu-id="09873-179">Instalar las dependencias de Hola BlueZ:</span><span class="sxs-lookup"><span data-stu-id="09873-179">Install hello BlueZ dependencies:</span></span>

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. <span data-ttu-id="09873-180">Descargar código fuente de hello BlueZ desde bluez.org:</span><span class="sxs-lookup"><span data-stu-id="09873-180">Download hello BlueZ source code from bluez.org:</span></span>

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="09873-181">Descomprima el código fuente de hello:</span><span class="sxs-lookup"><span data-stu-id="09873-181">Unzip hello source code:</span></span>

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. <span data-ttu-id="09873-182">Cambiar la carpeta de directorios toohello recién creado:</span><span class="sxs-lookup"><span data-stu-id="09873-182">Change directories toohello newly created folder:</span></span>

    ```sh
    cd bluez-5.37
    ```

1. <span data-ttu-id="09873-183">Configurar hello BlueZ código toobe integrada:</span><span class="sxs-lookup"><span data-stu-id="09873-183">Configure hello BlueZ code toobe built:</span></span>

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. <span data-ttu-id="09873-184">Cree BlueZ:</span><span class="sxs-lookup"><span data-stu-id="09873-184">Build BlueZ:</span></span>

    ```sh
    make
    ```

1. <span data-ttu-id="09873-185">Una vez que ha terminado la creación, instale BlueZ:</span><span class="sxs-lookup"><span data-stu-id="09873-185">Install BlueZ once it is done building:</span></span>

    ```sh
    sudo make install
    ```

1. <span data-ttu-id="09873-186">Cambiar la configuración de servicio systemd Bluetooth de forma que apunte toohello nuevo demonio de bluetooth en el archivo hello `/lib/systemd/system/bluetooth.service`.</span><span class="sxs-lookup"><span data-stu-id="09873-186">Change systemd service configuration for bluetooth so it points toohello new bluetooth daemon in hello file `/lib/systemd/system/bluetooth.service`.</span></span> <span data-ttu-id="09873-187">Reemplace la línea de 'ExecStart' de hello con hello siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="09873-187">Replace hello 'ExecStart' line with hello following text:</span></span>

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a><span data-ttu-id="09873-188">Habilitar conectividad toohello SensorTag dispositivo desde el dispositivo de frambuesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="09873-188">Enable connectivity toohello SensorTag device from your Raspberry Pi 3 device</span></span>

<span data-ttu-id="09873-189">Antes de ejemplo Hola en ejecución, debe tooverify que el 3 de Pi frambuesa puede conectarse toohello SensorTag dispositivo.</span><span class="sxs-lookup"><span data-stu-id="09873-189">Before running hello sample, you need tooverify that your Raspberry Pi 3 can connect toohello SensorTag device.</span></span>

1. <span data-ttu-id="09873-190">Asegúrese de hello `rfkill` utilidad se instala:</span><span class="sxs-lookup"><span data-stu-id="09873-190">Ensure hello `rfkill` utility is installed:</span></span>

    ```sh
    sudo apt-get install rfkill
    ```

1. <span data-ttu-id="09873-191">Desbloquear bluetooth en hello frambuesa Pi 3 y compruebe que es el número de versión de hello **5.37**:</span><span class="sxs-lookup"><span data-stu-id="09873-191">Unblock bluetooth on hello Raspberry Pi 3 and check that hello version number is **5.37**:</span></span>

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. <span data-ttu-id="09873-192">shell de tooenter Hola bluetooth interactivo, iniciar el servicio de bluetooth hello y ejecute hello **bluetoothctl** comando:</span><span class="sxs-lookup"><span data-stu-id="09873-192">tooenter hello interactive bluetooth shell, start hello bluetooth service and execute hello **bluetoothctl** command :</span></span>

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. <span data-ttu-id="09873-193">Escriba el comando hello **encendido** toopower controlador de hello bluetooth.</span><span class="sxs-lookup"><span data-stu-id="09873-193">Enter hello command **power on** toopower up hello bluetooth controller.</span></span> <span data-ttu-id="09873-194">comando de Hello devuelve siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="09873-194">hello command returns output similar toohello following:</span></span>

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. <span data-ttu-id="09873-195">En el shell de hello bluetooth interactiva, escriba el comando de hello **analizar en** tooscan para los dispositivos bluetooth.</span><span class="sxs-lookup"><span data-stu-id="09873-195">In hello interactive bluetooth shell, enter hello command **scan on** tooscan for bluetooth devices.</span></span> <span data-ttu-id="09873-196">comando de Hello devuelve siguiente toohello similar de salida:</span><span class="sxs-lookup"><span data-stu-id="09873-196">hello command returns output similar toohello following:</span></span>

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. <span data-ttu-id="09873-197">Asegúrese de dispositivo de hello SensorTag reconocible presionando botón pequeño hello (Hola debe parpadear LED verde).</span><span class="sxs-lookup"><span data-stu-id="09873-197">Make hello SensorTag device discoverable by pressing hello small button (hello green LED should flash).</span></span> <span data-ttu-id="09873-198">Hola frambuesa Pi 3 debe detectar dispositivos de hello SensorTag:</span><span class="sxs-lookup"><span data-stu-id="09873-198">hello Raspberry Pi 3 should discover hello SensorTag device:</span></span>

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    <span data-ttu-id="09873-199">En este ejemplo, puede ver esa dirección MAC de hello SensorTag dispositivo hello **A0:E6:F8:B5:F6:00**.</span><span class="sxs-lookup"><span data-stu-id="09873-199">In this example, you can see that hello MAC address of hello SensorTag device is **A0:E6:F8:B5:F6:00**.</span></span>

1. <span data-ttu-id="09873-200">Desactivar el análisis mediante la especificación de hello **examinar desactivar** comando:</span><span class="sxs-lookup"><span data-stu-id="09873-200">Turn off scanning by entering hello **scan off** command:</span></span>

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. <span data-ttu-id="09873-201">Conecte tooyour SensorTag dispositivo con su dirección MAC escribiendo **conectar \<dirección MAC\>**.</span><span class="sxs-lookup"><span data-stu-id="09873-201">Connect tooyour SensorTag device using its MAC address by entering **connect \<MAC address\>**.</span></span> <span data-ttu-id="09873-202">Después de la salida de ejemplo de Hola se abrevia para mayor claridad:</span><span class="sxs-lookup"><span data-stu-id="09873-202">hello following sample output is abbreviated for clarity:</span></span>

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > <span data-ttu-id="09873-203">Puede enumerar las características de GATT hello de dispositivo de hello utilizando Hola de nuevo **atributos de lista** comando.</span><span class="sxs-lookup"><span data-stu-id="09873-203">You can list hello GATT characteristics of hello device again using hello **list-attributes** command.</span></span>

1. <span data-ttu-id="09873-204">Ahora puede desconectarse de dispositivo de hello mediante hello **desconectar** comando y, a continuación, salir del shell de bluetooth hello mediante hello **salir** comando:</span><span class="sxs-lookup"><span data-stu-id="09873-204">You can now disconnect from hello device using hello **disconnect** command and then exit from hello bluetooth shell using hello **quit** command:</span></span>

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

<span data-ttu-id="09873-205">Ahora está muestra Bilitar IoT borde de Hola a toorun listo en el 3 de frambuesa Pi.</span><span class="sxs-lookup"><span data-stu-id="09873-205">You're now ready toorun hello BLE IoT Edge sample on your Raspberry Pi 3.</span></span>

## <a name="run-hello-iot-edge-ble-sample"></a><span data-ttu-id="09873-206">Ejecutar ejemplo de Hola IoT borde BLE</span><span class="sxs-lookup"><span data-stu-id="09873-206">Run hello IoT Edge BLE sample</span></span>

<span data-ttu-id="09873-207">ejemplo de Hola IoT borde Bilitar a toorun, necesita toocomplete tres tareas:</span><span class="sxs-lookup"><span data-stu-id="09873-207">toorun hello IoT Edge BLE sample, you need toocomplete three tasks:</span></span>

* <span data-ttu-id="09873-208">Configurar dos dispositivos de ejemplo en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="09873-208">Configure two sample devices in your IoT Hub.</span></span>
* <span data-ttu-id="09873-209">Compile IoT Edge en el dispositivo Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="09873-209">Build IoT Edge on your Raspberry Pi 3 device.</span></span>
* <span data-ttu-id="09873-210">Configurar y ejecutar el ejemplo de Hola a habilitar en el dispositivo de frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="09873-210">Configure and run hello BLE sample on your Raspberry Pi 3 device.</span></span>

<span data-ttu-id="09873-211">En tiempo de Hola de escritura, IoT borde sólo admite módulos BLE en puertas de enlace que se ejecutan en Linux.</span><span class="sxs-lookup"><span data-stu-id="09873-211">At hello time of writing, IoT Edge only supports BLE modules in gateways running on Linux.</span></span>

### <a name="configure-two-sample-devices-in-your-iot-hub"></a><span data-ttu-id="09873-212">Configuración de dos dispositivos de ejemplo en IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09873-212">Configure two sample devices in your IoT Hub</span></span>

* <span data-ttu-id="09873-213">[Crear un centro de IoT] [ lnk-create-hub] en su suscripción de Azure, se necesita Hola nombre de su toocomplete de base de datos central en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="09873-213">[Create an IoT hub][lnk-create-hub] in your Azure subscription, you need hello name of your hub toocomplete this walkthrough.</span></span> <span data-ttu-id="09873-214">Si no tiene ninguna, puede crear una [cuenta gratuita][lnk-free-trial] en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="09873-214">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="09873-215">Agregar un dispositivo denominado **SensorTag_01** tooyour centro de IoT y tome nota de su clave de identificador y el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="09873-215">Add one device called **SensorTag_01** tooyour IoT hub and make a note of its id and device key.</span></span> <span data-ttu-id="09873-216">Puede usar hello [explorador del dispositivo o el centro de IOT explorador] [ lnk-explorer-tools] herramientas tooadd este centro de IoT de toohello de dispositivo que creó en el paso anterior de Hola y tooretrieve su clave.</span><span class="sxs-lookup"><span data-stu-id="09873-216">You can use hello [device explorer or iothub-explorer][lnk-explorer-tools] tools tooadd this device toohello IoT hub you created in hello previous step and tooretrieve its key.</span></span> <span data-ttu-id="09873-217">Asignar este dispositivo toohello SensorTag dispositivo al configurar la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-217">You map this device toohello SensorTag device when you configure hello gateway.</span></span>

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a><span data-ttu-id="09873-218">Compilar Azure IoT Edge en Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="09873-218">Build Azure IoT Edge on your Raspberry Pi 3</span></span>

<span data-ttu-id="09873-219">Instale las dependencias para Azure IoT Edge:</span><span class="sxs-lookup"><span data-stu-id="09873-219">Install dependencies for Azure IoT Edge:</span></span>

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

<span data-ttu-id="09873-220">Siguiente de hello use comandos tooclone IoT borde y todos su submodules tooyour directorio particular de:</span><span class="sxs-lookup"><span data-stu-id="09873-220">Use hello following commands tooclone IoT Edge and all its submodules tooyour home directory:</span></span>

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

<span data-ttu-id="09873-221">Si tiene una copia completa de hello repositorio IoT borde en el 3 de Pi de frambuesa, puede compilar mediante Hola siguiente comando de carpeta de Hola que contiene Hola SDK:</span><span class="sxs-lookup"><span data-stu-id="09873-221">When you have a complete copy of hello IoT Edge repository on your Raspberry Pi 3, you can build it using hello following command from hello folder that contains hello SDK:</span></span>

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a><span data-ttu-id="09873-222">Configurar y ejecutar el ejemplo de Hola a habilitar sobre frambuesa Pi 3</span><span class="sxs-lookup"><span data-stu-id="09873-222">Configure and run hello BLE sample on your Raspberry Pi 3</span></span>

<span data-ttu-id="09873-223">toobootstrap y ejemplo de Hola de ejecución, debe configurar cada módulo IoT borde que participa en la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-223">toobootstrap and run hello sample, you must configure each IoT Edge module that participates in hello gateway.</span></span> <span data-ttu-id="09873-224">Esta configuración se proporciona en un archivo JSON y debe configurar los cinco módulos de IoT Edge participantes.</span><span class="sxs-lookup"><span data-stu-id="09873-224">This configuration is provided in a JSON file and you must configure all five participating IoT Edge modules.</span></span> <span data-ttu-id="09873-225">Hay un archivo JSON de ejemplo en el repositorio, Hola denominado **puerta de enlace\_sample.json** que puede usar como punto de partida para crear su propio archivo de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-225">There is a sample JSON file in hello repository called **gateway\_sample.json** that you can use as hello starting point for building your own configuration file.</span></span> <span data-ttu-id="09873-226">Este archivo se encuentra en hello **ble_gateway/samples/src** carpeta en la copia local de hello repositorio IoT borde.</span><span class="sxs-lookup"><span data-stu-id="09873-226">This file is in hello **samples/ble_gateway/src** folder in local copy of hello IoT Edge repository.</span></span>

<span data-ttu-id="09873-227">Hello las secciones siguientes describen cómo tooedit esta configuración de archivos de ejemplo de Hola Bilitar y asumir ese repositorio IoT borde hello es Hola **/home/pi/iot-edge /** carpeta frambuesa Pi 3.</span><span class="sxs-lookup"><span data-stu-id="09873-227">hello following sections describe how tooedit this configuration file for hello BLE sample and assume that hello IoT Edge repository is in hello **/home/pi/iot-edge/** folder on your Raspberry Pi 3.</span></span> <span data-ttu-id="09873-228">Si el repositorio de hello está en otra parte, ajustar las rutas de acceso de hello según corresponda.</span><span class="sxs-lookup"><span data-stu-id="09873-228">If hello repository is elsewhere, adjust hello paths accordingly.</span></span>

#### <a name="logger-configuration"></a><span data-ttu-id="09873-229">Configuración del registrador</span><span class="sxs-lookup"><span data-stu-id="09873-229">Logger configuration</span></span>

<span data-ttu-id="09873-230">Suponiendo que el repositorio de puerta de enlace de Hola se encuentra en hello **/home/pi/iot-edge /** carpeta, configurar el módulo de registrador de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="09873-230">Assuming hello gateway repository is located in hello **/home/pi/iot-edge/** folder, configure hello logger module as follows:</span></span>

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a><span data-ttu-id="09873-231">Configuración del módulo BLE</span><span class="sxs-lookup"><span data-stu-id="09873-231">BLE module configuration</span></span>

<span data-ttu-id="09873-232">configuración de ejemplo de Hola para dispositivos de hello Bilitar supone un dispositivo SensorTag de instrumentos Texas.</span><span class="sxs-lookup"><span data-stu-id="09873-232">hello sample configuration for hello BLE device assumes a Texas Instruments SensorTag device.</span></span> <span data-ttu-id="09873-233">Todos los dispositivos Bilitar estándar que pueden funcionar como un GATT periférico debe funcionan, pero puede que necesite característica GATT de hello tooupdate identificadores y los datos.</span><span class="sxs-lookup"><span data-stu-id="09873-233">Any standard BLE device that can operate as a GATT peripheral should work but you may need tooupdate hello GATT characteristic IDs and data.</span></span> <span data-ttu-id="09873-234">Agregue la dirección MAC de hello de dispositivo SensorTag:</span><span class="sxs-lookup"><span data-stu-id="09873-234">Add hello MAC address of your SensorTag device:</span></span>

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

<span data-ttu-id="09873-235">Si no usa un dispositivo SensorTag, revise la documentación de Hola de su toodetermine de dispositivo habilitar si necesita característica GATT de hello tooupdate identificadores y valores de datos.</span><span class="sxs-lookup"><span data-stu-id="09873-235">If you are not using a SensorTag device, review hello documentation for your BLE device toodetermine whether you need tooupdate hello GATT characteristic IDs and data values.</span></span>

#### <a name="iot-hub-module"></a><span data-ttu-id="09873-236">módulo de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="09873-236">IoT Hub module</span></span>

<span data-ttu-id="09873-237">Agregar nombre de Hola de su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-237">Add hello name of your IoT Hub.</span></span> <span data-ttu-id="09873-238">suele ser el valor de sufijo de Hello **devices.net azure**:</span><span class="sxs-lookup"><span data-stu-id="09873-238">hello suffix value is typically **azure-devices.net**:</span></span>

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a><span data-ttu-id="09873-239">Configuración del módulo de asignación de identidad</span><span class="sxs-lookup"><span data-stu-id="09873-239">Identity mapping module configuration</span></span>

<span data-ttu-id="09873-240">Agregar dirección MAC de Hola de su dispositivo SensorTag y el Id. de dispositivo de Hola y la clave de hello **SensorTag_01** dispositivo agregado tooyour centro de IoT:</span><span class="sxs-lookup"><span data-stu-id="09873-240">Add hello MAC address of your SensorTag device and hello device ID and key of hello **SensorTag_01** device you added tooyour IoT Hub:</span></span>

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a><span data-ttu-id="09873-241">Configuración de la impresora BLE</span><span class="sxs-lookup"><span data-stu-id="09873-241">BLE Printer module configuration</span></span>

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a><span data-ttu-id="09873-242">Configuración del módulo BLEC2D</span><span class="sxs-lookup"><span data-stu-id="09873-242">BLEC2D Module Configuration</span></span>

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a><span data-ttu-id="09873-243">Configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="09873-243">Routing Configuration</span></span>

<span data-ttu-id="09873-244">configuración siguiente Hello garantiza siguiente Hola enrutamiento entre módulos IoT borde:</span><span class="sxs-lookup"><span data-stu-id="09873-244">hello following configuration ensures hello following routing between IoT Edge modules:</span></span>

* <span data-ttu-id="09873-245">Hola **registrador** módulo recibe y registra todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="09873-245">hello **Logger** module receives and logs all messages.</span></span>
* <span data-ttu-id="09873-246">Hola **SensorTag** módulo envía Hola de mensajes tooboth **asignación** y **Bilitar impresora** módulos.</span><span class="sxs-lookup"><span data-stu-id="09873-246">hello **SensorTag** module sends messages tooboth hello **mapping** and **BLE Printer** modules.</span></span>
* <span data-ttu-id="09873-247">Hola **asignación** módulo envía mensajes toohello **el centro de IOT** toobe módulo enviada tooyour centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-247">hello **mapping** module sends messages toohello **IoTHub** module toobe sent up tooyour IoT Hub.</span></span>
* <span data-ttu-id="09873-248">Hola **el centro de IOT** módulo envía mensajes realizar copia de toohello **asignación** módulo.</span><span class="sxs-lookup"><span data-stu-id="09873-248">hello **IoTHub** module sends messages back toohello **mapping** module.</span></span>
* <span data-ttu-id="09873-249">Hola **asignación** módulo envía mensajes toohello **BLEC2D** módulo.</span><span class="sxs-lookup"><span data-stu-id="09873-249">hello **mapping** module sends messages toohello **BLEC2D** module.</span></span>
* <span data-ttu-id="09873-250">Hola **BLEC2D** módulo envía mensajes realizar copia de toohello **Sensor etiqueta** módulo.</span><span class="sxs-lookup"><span data-stu-id="09873-250">hello **BLEC2D** module sends messages back toohello **Sensor Tag** module.</span></span>

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

<span data-ttu-id="09873-251">ejemplo de Hola a toorun, archivo de configuración de JSON toohello ruta de acceso de hello pasada como un parámetro toohello **bilitar\_puerta de enlace** binario.</span><span class="sxs-lookup"><span data-stu-id="09873-251">toorun hello sample, pass hello path toohello JSON configuration file as a parameter toohello **ble\_gateway** binary.</span></span> <span data-ttu-id="09873-252">Hello siguiente comando presupone que usa hello **gateway_sample.json** archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="09873-252">hello following command assumes you are using hello **gateway_sample.json** configuration file.</span></span> <span data-ttu-id="09873-253">Ejecute este comando desde hello **iot borde** carpeta Hola frambuesa Pi:</span><span class="sxs-lookup"><span data-stu-id="09873-253">Execute this command from hello **iot-edge** folder on hello Raspberry Pi:</span></span>

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

<span data-ttu-id="09873-254">Puede que necesite toopress Hola pequeño situado en hello SensorTag dispositivo toomake se puede detectar antes de ejecutar el ejemplo hello.</span><span class="sxs-lookup"><span data-stu-id="09873-254">You may need toopress hello small button on hello SensorTag device toomake it discoverable before you run hello sample.</span></span>

<span data-ttu-id="09873-255">Al ejecutar el ejemplo hello, puede usar hello [explorador del dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) herramienta toomonitor Hola mensajes Hola puerta de enlace de IoT borde reenvía del dispositivo de SensorTag Hola.</span><span class="sxs-lookup"><span data-stu-id="09873-255">When you run hello sample, you can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toomonitor hello messages hello IoT Edge gateway forwards from hello SensorTag device.</span></span> <span data-ttu-id="09873-256">Por ejemplo, mediante el centro de IOT explorador puede supervisar mensajes de dispositivo a la nube mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="09873-256">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="09873-257">Envío de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="09873-257">Send cloud-to-device messages</span></span>

<span data-ttu-id="09873-258">módulo de Hello Bilitar también admite comandos envío del dispositivo toohello de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-258">hello BLE module also supports sending commands from IoT Hub toohello device.</span></span> <span data-ttu-id="09873-259">Puede usar hello [explorador del dispositivo](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) o hello [el centro de IOT explorador](https://github.com/Azure/iothub-explorer) mensajes JSON de herramienta toosend ese módulo de puerta de enlace de hello Bilitar reenvía en dispositivo de Bilitar toohello.</span><span class="sxs-lookup"><span data-stu-id="09873-259">You can use hello [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) or hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool toosend JSON messages that hello BLE gateway module forwards on toohello BLE device.</span></span>

<span data-ttu-id="09873-260">Si usa Hola Texas instrumentos SensorTag dispositivo, puede activar LED rojo hello, LED verde o timbre mediante el envío de comandos desde el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="09873-260">If you are using hello Texas Instruments SensorTag device, you can turn on hello red LED, green LED, or buzzer by sending commands from IoT Hub.</span></span> <span data-ttu-id="09873-261">Antes de enviar comandos desde el centro de IoT, en primer lugar enviar Hola siguientes dos mensajes JSON en orden.</span><span class="sxs-lookup"><span data-stu-id="09873-261">Before you send commands from IoT Hub, first send hello following two JSON messages in order.</span></span> <span data-ttu-id="09873-262">A continuación, puede enviar cualquiera de hello tooturn de comandos en las luces de Hola o timbre.</span><span class="sxs-lookup"><span data-stu-id="09873-262">Then you can send any of hello commands tooturn on hello lights or buzzer.</span></span>

1. <span data-ttu-id="09873-263">Restablecer todos los LED y timbre hello (desactivarlas):</span><span class="sxs-lookup"><span data-stu-id="09873-263">Reset all LEDs and hello buzzer (turn them off):</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. <span data-ttu-id="09873-264">Configure E/S como "remoto":</span><span class="sxs-lookup"><span data-stu-id="09873-264">Configure I/O as 'remote':</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

<span data-ttu-id="09873-265">Ahora puede enviar cualquiera de hello siguiente tooturn de comandos de las luces de Hola o timbre en dispositivo de Hola SensorTag:</span><span class="sxs-lookup"><span data-stu-id="09873-265">Now you can send any of hello following commands tooturn on hello lights or buzzer on hello SensorTag device:</span></span>

* <span data-ttu-id="09873-266">Activar LED Hola rojo:</span><span class="sxs-lookup"><span data-stu-id="09873-266">Turn on hello red LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* <span data-ttu-id="09873-267">Activar LED verde hello:</span><span class="sxs-lookup"><span data-stu-id="09873-267">Turn on hello green LED:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* <span data-ttu-id="09873-268">Activar el timbre hello:</span><span class="sxs-lookup"><span data-stu-id="09873-268">Turn on hello buzzer:</span></span>

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="09873-269">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09873-269">Next Steps</span></span>

<span data-ttu-id="09873-270">Si desea toogain conocimientos avanzados del borde de IoT y experimentar con algunos ejemplos de código, visite la página siguiente de hello tutoriales de desarrollador y recursos:</span><span class="sxs-lookup"><span data-stu-id="09873-270">If you want toogain a more advanced understanding of IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="09873-271">[Azure IoT Edge][lnk-sdk]</span><span class="sxs-lookup"><span data-stu-id="09873-271">[Azure IoT Edge][lnk-sdk]</span></span>

<span data-ttu-id="09873-272">toofurther explorar las capacidades de Hola de centro de IoT, vea:</span><span class="sxs-lookup"><span data-stu-id="09873-272">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="09873-273">[Guía para desarrolladores de IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="09873-273">[IoT Hub developer guide][lnk-devguide]</span></span>

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
